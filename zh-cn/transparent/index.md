# 使用RDKit生成无背景的化学结构式--附Python代码


**前言**

笔者发现传统的用RDKit画图画出来有白色背景，放在PowerPoint里面很不爽。参考了[这一篇文献](https://link.springer.com/article/10.1186/s13321-022-00664-x)找到了代码。

```python
from rdkit import Chem
from rdkit import rdBase
from rdkit.Chem import Draw
from rdkit.Chem.Draw import rdMolDraw2D
from rdkit.Chem import rdDepictor
rdDepictor.SetPreferCoordGen(True)
from rdkit.Chem import rdMolDescriptors
from rdkit.Chem import rdFMCS
from rdkit import DataStructs
import io
from PIL import Image

def show_png(data):
    bio = io.BytesIO(data)
    img = Image.open(bio)
    return img
smi = "CCCCCC" #以环己烷为例
drawer = rdMolDraw2D.MolDraw2DCairo(300,300) #可以自行调整图像尺寸
drawer.drawOptions().clearBackground = False
drawer.drawOptions().addStereoAnnotation = False
drawer.DrawMolecule(Chem.MolFromSmiles(smi))
drawer.FinishDrawing()
mol = drawer.GetDrawingText()
show_png(mol)
```

右键保存即可得到透明的png文件。
