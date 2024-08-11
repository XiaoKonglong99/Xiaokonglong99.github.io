# 使用ChEMBL Python API 搜索化合物信息


### 前言

ChEMBL 算是各位化学从业者喜闻乐见的数据库。~~（因为他不要钱）~~ 但是如果我们想要批量收集我们想要的内容，用网页版挨个寻找属实有点麻烦了。那么，有没有什么方法能够**批量** 且**自动**获取我们想要的分子信息呢？

其实除了我们熟知的ChEMBL[网页](https://www.ebi.ac.uk/chembl/) ， ChEMBL 还贴心的提供了可以用Python 搜索的 ChEMBL web service client 服务。只要我们在Python代码中输入想要的关键词，就可以批量搜索到我们想要的内容然后保存为CSV 文件用于后续处理。~~（比如赛博炼丹）~~

#### 应用实例

一位励志发JACS的同学希望收集ChEMBL上**杂环化合物Heterocyclic compound**的 **溶解度Solubility**数据，我们应该怎么找呢？

**示例代码**：

首先 安装chembl_webresource_client 包

```bash
! pip install chembl_webresource_client
```

然后运行这一段代码

```python
import csv
from chembl_webresource_client.new_client import new_client

# 新建一个Client
client = new_client

# 录入关键词 solubility
assays = client.assay.filter(
    description__icontains='solubility'
)

# 新建一个CSV文件存储结果
with open('heterocyclic_solubility_data.csv', 'w', newline='', encoding='utf-8') as csvfile:
    fieldnames = ['CHEMBL_ID', 'SMILES', 'Solubility_value', 'Solubility_units', 'Solubility_doi', 'Assay_description']
    # 这里我们打算收集杂环分子的 ID，SMILES结构式，溶解度数据和单位，原始文献和这个数据的说明（比如测试条件），不需要的话可以按需删除
    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    writer.writeheader()

    
    for assay in assays:
        activities = client.activity.filter(assay_chembl_id=assay['assay_chembl_id'])
        for activity in activities:
            try:
                molecule = client.molecule.get(activity['molecule_chembl_id'])
                
                # 判断这个分子是不是杂环分子
                is_heterocyclic = False
                if molecule.get('molecule_structures'):
                    smiles = molecule['molecule_structures'].get('canonical_smiles')
                    if smiles and any(atom in smiles for atom in ['n', 'o', 's', 'p','se']):
                        is_heterocyclic = True
                if is_heterocyclic:
                    try:
                        document = client.document.get(activity['document_chembl_id'])
                        doi = document.get('doi', "Not Available")
                    except Exception:
                        doi = "Not Available"
                    # 储存结果
                    writer.writerow({
                        'CHEMBL_ID': activity['molecule_chembl_id'],
                        'SMILES': smiles,
                        'Solubility_value': activity.get('value', "Not Available"),
                        'Solubility_units': activity.get('units', "Not Available"),
                        'Solubility_doi': doi,
                        'Assay_description': assay.get('description', "Not Available")
                    })
            except Exception as e:
                print(f"Error processing molecule {activity['molecule_chembl_id']}: {str(e)}")
                continue

print("Data collection completed. Results saved in 'heterocyclic_solubility_data.csv'.")
```

然后我们就能看到我们想要的结果了

#### 注意事项

- ChEMBL 上面的数据均为人肉收集和录入，请务必使用之前人工验证
- 这一个过程可能持续很长一段时间，建议在程序运行过程中多多摸鱼

Good Luck！

**参考文献**：[Davies et al.,2015](https://academic.oup.com/nar/article/43/W1/W612/2467881)

