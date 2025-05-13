# Searching Compound Information Using ChEMBL Python API

### Introduction
ChEMBL is a database beloved by chemistry professionals. ~~~~(Because it's free)~~~~ However, if we want to collect information in bulk, searching individually through the web interface can be quite troublesome. So, is there a method to obtain molecular information **in bulk** and **automatically**?

Actually, besides the well-known ChEMBL [website](https://www.ebi.ac.uk/chembl/), ChEMBL thoughtfully provides a ChEMBL web service client that can be used with Python. By simply entering the desired keywords in Python code, we can search in bulk for the content we need and save it as a CSV file for subsequent processing. ~~~~(For example, cyber alchemy,aka Machine Learning)~~~~

### Application Example
An aspiring JACS author wants to collect **solubility** data for **heterocyclic compounds** from ChEMBL. How should we approach this?
**Example code**:
First, install the chembl_webresource_client package

```bash
! pip install chembl_webresource_client
```

Then run this code


```python
import csv
from chembl_webresource_client.new_client import new_client

# Create a new Client
client = new_client

# Enter the keyword 'solubility'
assays = client.assay.filter(
    description__icontains='solubility'
)

# Create a new CSV file to store the results
with open('heterocyclic_solubility_data.csv', 'w', newline='', encoding='utf-8') as csvfile:
    fieldnames = ['CHEMBL_ID', 'SMILES', 'Solubility_value', 'Solubility_units', 'Solubility_doi', 'Assay_description']
    # Here we plan to collect the ID of heterocyclic molecules, SMILES structure, solubility data and units, original literature, and description of this data (such as test conditions), which can be deleted as needed

    writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
    writer.writeheader()

    
    for assay in assays:
        activities = client.activity.filter(assay_chembl_id=assay['assay_chembl_id'])
        for activity in activities:
            try:
                molecule = client.molecule.get(activity['molecule_chembl_id'])
                
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

Then we can see our desired results.


#### Notes

- The data on ChEMBL is manually collected and entered, so please manually verify before use
- This process may take a long time, so it's recommended to take breaks during program execution
Good Luck!


**Reference**：[Davies et al.,2015](https://academic.oup.com/nar/article/43/W1/W612/2467881)

