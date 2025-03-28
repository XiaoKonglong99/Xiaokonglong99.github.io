# Advanced Molecular Modelling Applied to Drug Discovery(3FK181)，Uppsala University Exam Preparation Notes

# Advanced Molecular Modelling Applied to Drug Discovery(3FK181)，Uppsala University Exam Preparation Notes- 2023

---
## Note 
这是一个个人的备考复习笔记，适用于瑞典🇸🇪乌普萨拉大学的课程 [Advanced Molecular Modelling Applied to Drug Discovery(3FK181)，Uppsala University](https://www.uu.se/en/study/syllabus?query=41298).手写笔记由 [Claude AI](https://claude.ai)转换为Markdown格式， 仅供参考。

原始文档可点击[这里](https://drive.google.com/file/d/1uE6zOciSGgnXPS1vmfuWLrCtRQ5LIVrw/view?usp=share_link)下载
## Chapter 1: Ligand-Protein Interaction

### Key Points:
1. **Describing the interaction of molecules**
   - Determining if a molecule is a good target or not

2. **Types of Interactions**:
   - **Electrostatics**: Follow Coulomb's Law
     - F = -q₁q₂/4πε₀r² (ε₀: electric constant, q₁, q₂: charges)
     - π-π stacking: interactions between benzene rings
     - π-cation interactions: e.g., AchE with -NH₃⁺ and -Ph groups

   - **H-bond**: Consider O, N atoms
     - Mention HBD (hydrogen bond donors): -OH, -NH₂
     - HBA (hydrogen bond acceptors): C=O, C≡N (有供氢的)

   - **Halogen bond**: Cl···O, Br···O, I···O
     - No F bonds; if there is a -OF₃ group, it shows hydrophobic effect

   - **Polarization**: Charge redistribution when molecules approach each other
     - Charge → Dipole
     - Dipole → Dipole
     - Dipole-Dipole Interaction → Polarization → London Dispersion
     - Not generally included in molecular mechanics

   - **London Dispersion**: Dispersive forces (色散力)
     - π-stacking interactions

3. **Covalent Bond**:
   - **Advantages**:
     - Potency
     - Selectivity
     - PD (Pharmacodynamics)
   - **Risks**: Toxicity
   - **Explanation**:
     - **Potency**: Interaction is irreversible, very stable
     - **Selectivity**:
       - Can interact with specific proteins
       - Afatinib: Irreversibly binds certain proteins
     - **PD**: Not requiring high blood concentration; takes a long time
     - **Toxicity**: Off-target effects, irreversible

4. **Hydrophobic effect**: An entropic effect (熵的)
   - Gains potency but reduces solubility
   - Order of the dynamic hydrogen bond in water to accommodate a non-polar solute

5. **Considerations for L-P (Ligand-Protein) interaction**:
   - Size
   - Shape
   - Exposure (暴露外表的景象)
   - Hydrophilic/Hydrophobic properties
   - Ligandability/Druggability
   - Flexibility

6. **Relative Strength of Interactions**:
   - Covalent > Electrostatic > H-bond > van der Waals
   - 力的作用力大小

---

## Chapter 2: Molecular Dynamic Simulation

### I. Why Simulation
1. Study larger biological systems
2. Calculate movement as a function of time
3. Predict and explain outcomes of biological experiments
   - Example: Butane (丁烷) conformational analysis → Peptide folding

### II. Molecular Mechanics Approximation
1. Ignore electron motion
2. Born-Oppenheimer approximation: Separate electron and nuclear movements
3. Use Newton's laws to describe the system
4. Apply small molecule parameters to larger systems

### III. Van der Waals Force
- Repulsive then attractive
- UVdW = 4ε[(σ/r)¹² - (σ/r)⁶]
  - σ: Collision diameter
  - ε: Well depth
- Non-bonded interaction

### IV. For Charged Molecules
- UC = q₁q₂/4πε₀r₁j
- Very expensive to calculation

### V. Bond Potential (Hooke's Law)
- Accurate Morse potential typically replaced with simpler harmonic function (简谐函数)
- Bond: U = k₁/2(r-r₀)²
- Angle: U = k₂/2(θ-θ₀)²

### VI. Consider Partial Charges
- Water: partially charged → Water models: TIP3P, SPC

### VII. Consider Torsional Potential (扭转势能)
- U(φ) = Σ(k_n/2)[1+cos(nφ-φ₀)]
  - n = number of minima
  - 若有3个 minimal, n=3, φ₀=0
  - U(φ) = k₁/2[1+cos(φ)] + k₂/2[1+cos(2φ)] + k₃/2[1+cos(3φ)]

- **Problems**:
  1. Complex shape
  2. Relatively weak
  3. Torsion may lead to large changes to the whole system
  - Addition: Improper dihedrals → keep 4 atoms in a plane

- **Total energy function**:
  U = 4ε[(σ/r)¹² - (σ/r)⁶] + q₁q₂/4πε₀r₁j + k₁/2(r-r₀)² + k₂/2(θ-θ₀)² + Σ(k_n/2)[1+cos(nφ-φ₀)] + k₃/2(ξ-ξ₀)²

### Summary of Force Field
- It's empirical! (经验上)
1. There is no correct way to derive a force field; experimental data improves it
2. Fits reality, not theory - aim is to reproduce experimental results, not calculate it
3. Predict, not explain
4. Consider computational time; the best model isn't always chosen

### Biomolecular Simulation
#### VIII. AMBER
- Assisted model building with energy refinements
- Helps with:
  - Bond stretching, angle bending, dihedral torsional angles
  - Interaction with other models
  - Structure

### Force Field Summary
1. Force field is simplified and empirical (经验上)
2. Form and parameters differ in different models
3. Usefulness depends on the question being asked
4. Major problem: Bonds cannot be broken
5. Transferability of parameters is unclear
   - The ability to transfer parameters from one molecule to another (参数的转移性)
   - Assumption: similar molecules have the same parameters
   - Even if they have similar structure
   - Consider environment, temperature, and other molecules
6. Polarization is not included
7. General methods of generating parameters are still under development

### Modeling Complex Biomolecules
- Formula combines bond energies, angle energies, torsional terms, improper terms, electrostatic and VDW terms
- We have force field parameters for amino acids
- What about larger biomolecules?

### Free Energy vs Potential Energy
- The minimum potential energy state need not be the most popular state; free energy is
- G = H - TS → Entropy
- Enthalpy considerations
- Take average of a huge number of particles
- Experiment observation based on a single configuration

### Time Average
- < A > = (1/τ)∫₀ᵗ A(r^N(t), p^N(t))dt
- r: position; p: momenta; of all particles N
- (粒子位置和动量), τ→∞, 平均即为实际

### Statistical Thermodynamics
- Know the probability of every state
- n_i = N·(e^(-βE_i)/Σⱼe^(-βE_j))
  - n_i: number in a state
  - 利用"概率"
- Ergodic hypothesis (遍历假设): Time average = Ensemble average

### Sampling an Energy Landscape
- MD Simulation uses:
  - Newton's laws
  - Time dependence
  - Time average
  - Dynamical events

### Molecular Dynamics Simulation (分子动力学 Force Field)
1. Try to calculate the path of individual particles
2. Errors occur but final results are acceptable
3. Calculate motion as a function of time

### MD Process
1. Start with a set of coordinates
2. Calculate potential and force (用时时所迭)
3. Calculate acceleration: a_i = F_i/m_i
4. Calculate velocity and position: v + dt

### Leap-Frog Algorithm
- Calculate new coordinates for atoms (迭代算法)
- r_i(t+dt) = r_i(t) + dt·v_i(t+dt/2)

### For Trajectory (轨迹)
1. Different time series of snapshots
2. In theory, MD simulation is deterministic (确定性的)
   - If we know the state, we can predict behavior
3. In practice, errors accumulate
4. Looking over long time provides a good picture

### How to Choose Time Step
1. Must be small but not too small (need more to reach 1ms simulation)
2. If step is too big → unreasonable positions
3. Determined by the fastest vibration in system
4. Typically choose 1-2 fs

### Solvation in MD
1. Vacuum: No solvent, problematic
2. Implicit solvent model:
   - Replaced by average behavior of water
   - Analytical, so calculations are fast
   - Disadvantage: Only electrostatics in this expression
   - Other effects like entropy must be added separately

3. SBC (Spherical Boundary Condition):
   - Add water near the place of interest
   - Save time if not considering whole protein
   - Should restrain water inside the spherical boundary
   - Should add right polarization

4. PBC (Periodic Boundary Condition):
   - Create "infinite" system by creating identical copies
   - Use a periodic cell shape and cut-offs
   - When we define a "primary cell", we copy it
   - When an atom reaches edge, it enters from another side
   - Advantage: Use less atoms to simulate a large system
   - Computationally expensive

### Common Ensembles
1. NVT (Canonical): Control T (等容等温)
2. NPT (Isobaric-Isothermal): Control T & P (等压等温)
   - Temperature → Kinetic energy → Velocity

### Limitations of MD
1. Parameters are not perfect
   - Amino acid solvent free energy: ~1kJ/mol
   - Impossible to calculate binding energy more accurately
2. Phase space not fully sampled (相空间未完全采样)
3. Limited polarization effects (极化限制):
   - Water reorientation
   - Partial charge is fixed (The orientation change)

### MD Workflow
Get structure → Fix structure → Prepare topology → Add water → Energy min. → Equilibration phase → Run → Analysis

### MD Outcomes
- Doesn't mean it's "real"
- Everything is about statistics
- Error? A signal event is not

---

## Chapter 3: Free Energy

### I. Free Energy Basics
- ΔG<0: Reaction is spontaneous (自发的)

### II. Absolute Free Energy Calculation
- Hard/impossible to calculate directly
- Need to sample all parts of phase space
- Typical simulations only sample low-energy regions

### III. Thermodynamic Perturbation (干扰)
- F_A→B = F_B - F_A = -k_B·T·ln(Q_B/Q_A)
- Zwanzig's Formula: F_A→B = -kT·ln<e^(-ΔH/β)>_A
- How to use Zwanzig's Formula:
  - Calculate ΔG to go to B
  - Potential Energy of A and B (势能)
- Assumption: A-B gap is not big

### IV. Thermodynamic Cycle
- Path not necessary to be meaningful
- A → B → C → D: ΔG_AB + ΔG_DA - ΔG_CB - ΔG_DC = 0

### V. Fixing the Overlap Problem
- H(λ) = (1-λ)H_A + λH_B
  - λ is interpolation parameter (加入λ为中间态)
- F_B - F_A = (F_λ=0.5 - F_λ=0) + (F_λ=1 - F_λ=0.5)

### VI. Solvation Process
- ΔG_Sol = ΔG_VdW + ΔG_Charge + ΔG_Cav
  - VdW: van der Waals interaction between L-J atoms
  - Charge: Electrostatics
  - Cav: Cost for creating cavity in water (surface/entropy)

### VII. Thermodynamic Integration (积分)
- ΔF = ∫₀¹<H_B - H_A>_λ dλ

### VIII. Inhibitor Design
- If we know an inhibitor, we want a similar one (I = protein)
- 用于创新设计算法
```
I+E → I'+E'
↑     ↑
I     I'
```
- F_I→I'_bind - F_I→I'_bind = F_I→I'_bound - F_I→I'_Free

---

## Chapter 4: Quantum Chemistry

### I. Why Quantum Chemistry?
1. No parameters required
2. Explicit treatment of electrons
   - In principle, everything can be modeled:
   - Polarization, reactions, spectroscopy

### II. Postulates of Quantum Mechanics
1. State of quantum mechanical system completely specified by wavefunction Ψ(r,t)
   - r: vector in 3D space (三维空间的一个方向量)
   - t: time
   - Born Interpretation: Square of wave function → probability of finding the system at given values of the variable
   - p(x₁,x₂) = ∫|Ψ(x)|²dx
   - 概率

2. For every observable in classical mechanics, there is an operator in QC
   - (把传统力学量用量子算符表达互联系起来)

3. In any measurement of the observable associated with operator Â, the only values ever observed are the eigenvalues a
   - ÂΨ = aΨ
   - Â为物理量, Â对应于ψ, 则Â的a作用于ψ, 则Âψa

4. It can be averaged:
   - < A > = ∫Ψ*ÂΨdτ/∫Ψ*Ψdτ

5. Schrödinger Equation:
   - Time-dependent: ÂΨ(r,t) = iℏ∂Ψ(r,t)/∂t
   - For time-independent systems: (Â-E)Ψ(r) → the system's eigenvalues

### Born-Oppenheimer Approximation
1. Assumes m_nuclei >> m_electron
   - Electrons move faster
   - Electrons adjust immediately to nuclear movement
   - The operator of electrons doesn't include the kinetic of nuclei (动核近似)
   - H_e = T_e + V_ee + V_en + V_nn

2. Separation of Variables
   - n electrons moving independently: Ψ = ΠΦᵢ
   - E = ΣEᵢ

3. Pauli Principle and Slater Determinant
   - Pauli exclusion principle: Two or more electrons cannot occupy the same quantum state
   - (一个电子不可处于同一量子态)
   - Slater determinant: Follow the Pauli principle
   - When two electrons exchange location, wavefunction changes sign
   - For n=2 electrons: Ψ = (1/√2)|Φ₁(1) Φ₂(1)| / |Φ₁(2) Φ₂(2)|
   - Consequences of Slater determinant:
     - Follow electron Pauli principle
     - Consider electron correlation
     - Consider charge exchange

### Disadvantages
- Not always accurate
- Cannot explain correlation energy
- Computationally difficult

### III. Hartree-Fock / Self-Consistent Field
1. Slater determinant provides mathematical framework → Hartree-Fock
2. Hartree-Fock calculates the energy of a system (能量)
3. More accurate than simpler methods (更为准确)
4. Hartree-Fock uses basis sets to construct wavefunctions, then adjusts to reality
5. To choose basis sets:
   - Atomic nuclei as centers
   - Mix and match these functions
   - Base: Solution of Schrödinger equation of H
   - Radial part is Slater-type orbital (STO) - an exponential function
   - Use Gaussian functions (GTOs) to approximate

6. How many basis sets?
   - One independent minimal set
   - For reasonable results: at least 2 or 3
   - Add flexibility: add polarization
   - For anions: diffuse functions

7. Split Valence Basis Sets (价层分裂):
   - Valence electrons are more important
   - Use more functions on valence electrons
   - 6-31G(d,p) notation:
     - 6: inner shell electrons represented by 6 Gaussian-type orbitals
     - 3,1: valence shell represented by 3 GTOs for first part, 1 GTO for second
     - d,p: polarization functions (d for heavy atoms, p for hydrogen)

8. Limits of Hartree-Fock:
   - Adding more basis sets is always better
   - In H-F theory, electron-electron interactions treated with mean-field approach (平均场)
   - In reality, electron movement is correlated
   - Missing: Electron correlation energy (能量) 相关性

9. Post-Hartree-Fock:
   - Correlation effects approximated by including additional determinants
   - CI, MCSCF, MPn methods available

### IV. Density Functional Theory
1. Energy is a function of electron density:
   - E = F[ρ(r)] where ρ is density, F is a functional
   - Don't need to solve Schrödinger function
   - Only 3N variables needed
   - Hohenberg-Kohn theorem states the function "EXISTS" but doesn't specify what it is

2. We know it includes these parts:
   - E[ρ] = T[ρ] + E_ne[ρ] + E_ee[ρ]
     - T[ρ]: Kinetic energy of electrons
     - E_ne[ρ]: Attraction between nuclei and electrons
     - E_ee[ρ]: Repulsion between electrons
   - E[ρ] = T[ρ] + E_ne[ρ] + J[ρ] + K[ρ]
     - J[ρ]: Coulomb interaction (库仑项)
     - K[ρ]: Exchange term to fit Pauli exclusion principle (交换项)

3. Kohn-Sham Approach:
   - According to Heisenberg uncertainty principle, we cannot test momentum and location at the same time
   - (测不准原理不确定性原理)
   - P为运动量，对应位置，教授动能
   - Need to know velocity → 方程式
   - Hartree-Fock can calculate kinetic energy
   - For Kohn-Sham approach in DFT, add "fake" electrons to get approximate kinetic values

4. DFT in Practice:
   - E[ρ] = T_s[ρ] + E_ne[ρ] + J[ρ] + E_xc[ρ]
   - T_s[ρ]: Kinetic energy from Kohn-Sham orbitals
   - E_xc[ρ]: Other quantum mechanical effects (correlation)
   - Kohn-Sham simplified the function to T_s[ρ] + E_xc[ρ]
   - E_xc[ρ] is hard to calculate
   - Common functionals: B3LYP, 6-31G
   - Balance quality and computational cost

5. Dispersion in DFT:
   - Though dispersion is weak, it increases quickly in larger systems
   - Short distance: electron correlation included in functionals
   - Long distance not included
   - Most functionals fail to represent dispersion at all distances
   - Modern functionals (Minnesota family) take this into account

6. DFT in Drug Design:
   - Parameter generation for small molecules

7. Semi-Empirical Method (半经验方法):
   - These methods require too much computational time
   - Strategies to reduce computation:
     - Reduce number of functions
     - Reduce number of integrals (积分)
   - Approximations made to Hartree-Fock:
     - Core electrons ignored; only consider valence electrons with effective charge Z_eff
     - Only minimal basis set employed
     - Integrals involving more than two centers neglected
     - Remaining integrals are parameterized

8. Neglect Diatomic Differential Overlap approximation:
   - Examples: PM3, PM6, PM7

### V. Applying QC (Quantum Chemistry)
1. Energy Landscape:
   - QC bonds are a consequence of PES, not input parameters
   - Different molecules can be part of the same PES

2. Transition State Theory:
   - Reaction coordinate: lowest pathway from reactant to product
   - Transit state: max energy of reaction coordinate
   - This state/enzyme must be stable

3. Geometry Optimization:
   - For force fields, minimum energy when gradient becomes close to zero (energy minimum)
   - For QC:
     - Several maxima/minima
     - Optimization to saddle points
   - Curvature calculation needed (曲率)
   - Hessian Matrix: Contains all second derivatives
     - For energy minimum, all eigenvalues are positive
     - For transition state, one eigenvalue is negative
     - For second-order saddle point, two eigenvalues are negative / opposite sign

4. Hessian Matrix and Spectroscopy:
   - Hessian matrix used to understand vibration
   - If molecular vibration is harmonic, we can solve Schrödinger equation
   - E_vib = ℏ(n+½)√(k/μ), n = energy level
   - Between different energy levels → spectroscopic transition

5. Isotope Effect (同位素):
   - Start from E⁰_vib = ½ℏ√(k/μ) where μ is reduced mass
   - For H and D as example:
     - E⁰_H > E⁰_D, so ΔE_H < ΔE_D
     - In drug design: -O-CH₃ → -O-CD₃
     - Metabolized slowly, less frequent dosing

6. Enthalpies and Free Energy:
   - QC energy results include:
     - Electrons at 0K
     - Electrons and nuclei strictly separated
   - Absolute energy not useful; compare to others with same electron and nuclei configurations, using same method and basis set
   - Electronic energy → Enthalpies considering thermal energies (translation, rotation, vibration)

---

## Chapter 5: Cheminformatics

### I. Different Databases
Database comparison:

| Database             | Pros                                  | Cons                                    |
|----------------------|---------------------------------------|----------------------------------------|
| SciFinder/eMolecule  | Variety from multiple sources         | Inconsistency: Different sources may have different expressions |
|                      | Verified data, commercially available | Cost: Pay for subscription              |
| GDB-17               | Huge database                         | Too large to search effectively         |
|                      | Creative: may include molecules not synthesized yet | May not be able to be synthesized |
| Single Vendor (Enamine/ChemDiv) | Consistency: Same expression format | Limited diversity                      |
|                      | Quality data                          | Dependence: rely on single vendor for data |

### II. Cheminfo Selection
1. Pre-clean the Database:
   - Remove wrong structures
   - Remove salt and inorganic compounds
   - Remove duplicated and tautomers
   - Manual inspection, remove obvious unreasonable data

2. General Chemical Prototyping:
   - Compare active compounds if available
   - Exclude toxic structures and structures leading to similar analogues
   - Consider hydrophobic cores, rotatable bonds if target is known
   - Remove reactive functional groups (ensure selectivity)
   - Remove PAINS (Pan-Assay Interference Compounds) to ensure druggability
   - Create analogues to test affinity with docking

3. Diversity: PCA with physical chemical parameters, clustering

4. If high affinity is found, use it as a lead compound considering:
   - Size
   - Flexibility
   - Lipophilicity

---

## Chapter 6: Virtual Screening

### I. Virtual Screen vs. High-throughput Screening
Comparison:

| Aspect        | HTS (Physical)     | VS (Virtual)      |
|---------------|-------------------|-------------------|
| Location      | Lab               | Computer          |
| Time          | Days to weeks     | Hours to days     |
| Cost          | High              | Low to medium     |
| Compounds     | 10³-10⁶           | 10⁷-10¹²          |
| Data Generate | Experimental      | Theoretical       |

### II. Virtual Screen Methods
- Docking: Glide
- Pharmacophore search: Phase
- Shape similarity: ROCS
- Electrostatic similarity: EON

### III. Ligand Efficiency
- LE = ΔG/N_non-H, where ΔG = -RTlnKd
1. Smaller size means higher affinity to dock the target
2. High efficiency means more druggability, more stable
3. Normalized potency of a hit

### IV. Negative and Positive Design
- **Negative Design**: Avoid undesired properties (e.g., toxicity)
- **Positive Design**: Attempt to engineer molecules with desired properties

Process:
1. Weeding Out (Negative design):
   - Drug likeness
   - In silico ADMET
   - Frequent hitters
   - Reactive groups

2. Narrowing Down (Positive design):
   - Trend vectors
   - Substructural analysis
   - Similarity searching
   - Profile/landscape analysis (size, electrostatics, HBD/HBA)

3. Focusing In:
   - Structural based models
   - Advanced pharmacophore models
   - Informed docking
   - Informed design

### V. Frequent Hitters and Promiscuous Binders
1. Frequent hitters: Show activity in many assays; unspecific binding, aggregate, auto-fluorescence. May not be bioactive.
2. Promiscuous binders: Subset of frequent hitter. Can interact with many targets. Bioactive!

### VI. Benchmark Data Sets
1. Decoy: Has similar chemical structure as active compounds but doesn't have chemical activity. Use as negative controls in VS.
2. DUD: Directory of decoys, BRAD for ligand-base
3. MUV (Maximum Unbiased Validation): Collection of benchmark datasets
   - DUD: OK for docking
   - MUV: If we want minimal bias
4. Bias: May be easy to select similar molecules but not normal ones

5. Process to create own database benchmark:
   1. Create a goal/purpose
   2. Collect active compounds
   3. Collect inactive compounds (ZINC Database → "drug-like")
   4. Ensure diversity with different structures
   5. Split data into training and validation sets
   6. Test the method

### VII. Data Fusion
- Sum rank, rank vote, sum score
- EF = (tp/(tp+fp))/(A/T)
- Pareto rank
- Test EF 1%, EF 10%

### VIII. Problems with Decoys
1. Random compounds, decoys data should be similar, cannot divide the active compounds
2. Too similar: Hard to divide and may cause bias
3. From DUD: Some inactive may have active to other target

---

## MD & QC Summary

### I. Why MD vs Why QC
**MD Purpose**:
- Study biological systems
- Calculate with function of time
- Predict and explain outcomes of biological experiments

**QC Purpose**:
- No additional parameters required
- In theory, everything can be calculated

### II. MD Approximation vs QC Postulates
**MD Approximations**:
- Ignore electron motion
- Separate electron and nuclei
- Use Newton's law
- Transfer parameters from small to large molecules

**QC Postulates**:
- Wavefunction Ψ(r,t), Born's interpretation (解释)
- For every observation, an operator
- For every operator, eigenvalues
- Schrödinger's equation

### III. Force Field Advantages/Disadvantages
1. Force Field is simplified and empirical (经验上)
2. Form and parameters differ in different models
3. Usefulness depends on questions asked
4. Major problem: bonds cannot be broken
5. Transferability of parameters unclear
6. Polarization not considered
7. General methods still developing

### IV-V. MD Simulation Process
1. Try to calculate the path of each individual
2. Newton's law
3. May have errors
4. Add-up errors may be OK
5. Calculate motion as function of time

### VI. Limits of MD
1. Parameters not perfect
2. Phase space not fully sampled
3. Limited polarization effects (极化效果)

### VII. QC Approaches
- Schrödinger Equation: H(r,t) = EΨ(r,t)
- Pauli exclusion principle and Slater determinant
- With Slater determinant + Basis Set → Hartree-Fock
- Using GTO, STO-nG models (STO-3G means STO approximated by 3 GTOs)
- Hartree-Fock uses mean-field approach, but electrons' interaction is correlated
- Post Hartree-Fock: CI, MPn
- Density Functional Theory: No need to solve Schrödinger, only 3N
- DFT = E[ρ] = T_S[ρ] + E_ne[ρ] + J[ρ] + E_xc[ρ]
- DFT principle accurate; HF is not
- But we still don't know the expression of E_xc[ρ]
- Choose B3LYP/6-31G to balance quality and cost
- Semi-Empirical Method: Reduce number of functions/integrals
- Model PMx (x=3,6,7)
- Hessian Matrix: Contains all second derivatives
- For energy min: all eigenvalues positive
- For TS: one eigenvalue negative
- A second-order saddle point: two eigenvalues negative
- Also in spectroscopy: E_vib = ℏ(n+½)√(k/μ)
- Isotope effect

### Words List
- Electrostatic: 电力
- π-stacking
- Halogen Bond
- London Dispersion: a 色散力
- Pauli Repulsion: 泡利(排斥)
- Entropic: 熵的
- Enclosure/Exposure: 暴露外表的景象
- Torsional Potential: 扭转势能
- Ensemble Average: 总体~
- Ergodic hypothesis: 遍历假设
- Ensemble average = Time average
- Trajectory: 轨迹
- Implicit solvent model
- Canonical Ensembles: 等温
- Isobaric Ensemble
- Postulate: 假设
- Operator: 算子
- Eigenvalue: 特征值
- Spherical/Periodic

