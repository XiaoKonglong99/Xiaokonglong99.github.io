# Draw TRANSPARENT Chemical Structure with RDKit --With Python Code


### Background
It's hard to remove the white background of molecular 2D figures created directly with RDKit. They don't look good when placed in PowerPoint. [This article](https://link.springer.com/article/10.1186/s13321-022-00664-x) provided a way to make **TRANSPARENT** ones. 

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
smi = "CCCCCC" #Take cyclohexane as an example
drawer = rdMolDraw2D.MolDraw2DCairo(300,300) #You can adjust the image size
drawer.drawOptions().clearBackground = False
drawer.drawOptions().addStereoAnnotation = False
drawer.DrawMolecule(Chem.MolFromSmiles(smi))
drawer.FinishDrawing()
mol = drawer.GetDrawingText()
show_png(mol)
```

Right click and save it, done!
Cheers!🍺
