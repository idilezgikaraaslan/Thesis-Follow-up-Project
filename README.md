# Thesis Follow-up Project: Cosmic Birefringence Estimation with D-Estimators — A Numerical Extension

This repository contains a Python-based numerical extension of my Master's thesis:

**[Cosmic Birefringence with the CMB: A Harmonic-Based Methodology](https://hdl.handle.net/20.500.12608/79648)**  
MSc in Astrophysics and Cosmology — University of Padova

This project aims to implement and validate the harmonic-space **D-estimators** derived analytically in the thesis using simulated Cosmic Microwave Background (CMB) polarization maps and power spectra.

---

## Abstract of the Thesis

This thesis explores parity-violating extensions of standard electromagnetism, which can be realized through a Chern-Simons term coupling the dual of the electromagnetic tensor to a scalar field (or pseudo-scalar field, such as an axion-like field) where the latter may act as dark matter or dark energy. This interaction rotates the linear polarization of light in a manner similar to birefringent materials and is therefore commonly referred to as the **Cosmic Birefringence (CB)** effect. 

Since the Cosmic Microwave Background (CMB) is linearly polarized due to Thomson scattering at the last scattering surface, the CMB is often used to probe this phenomenon. In fact, recent analyses on Planck data have intriguingly hinted at a detection of CB with a statistical significance ranging from 2.4 to 3.6 sigma. These measurements have attracted significant attention in recent years, as they hold the potential to uncover new physics beyond the standard model of particle physics and cosmology.

In this thesis, we compute how CB affects the CMB angular power spectra. Additionally, we analytically derive two harmonic-based estimators, known in the literature as **D-estimators**, which constrain the CB effect by utilizing information from the TB (temperature anisotropies and B-mode polarization) and EB (E- and B-mode polarization) CMB angular power spectra. We verify that these estimators correctly recover the birefringence angle and assess their expected statistical efficiency, recovering known results from the literature. Additionally, we perform a detailed analysis of the joint estimator, obtained by combining the two D-estimators, and provide an analytical expression for the total joint uncertainty. While it is known that the joint estimator is dominated by the one derived from the EB spectrum, the final expression for the combined estimator can be considered new.

---

## Project Description

This project uses a simulation-based pipeline to evaluate the performance of D-estimators for measuring the birefringence angle $\beta$ in the Cosmic Microwave Background (CMB).

Key steps include:

1. **Loading Planck Fiducial CMB Spectra**  
   Theoretical spectra (TT, EE, BB, TE) are loaded from Planck 2018 data and converted to $C_\ell$.

2. **Generating Simulated CMB Maps**  
   Simulated full-sky maps of T, Q, and U are generated using `healpy.synfast` for a given angular power spectrum. A total of 100 realizations are produced to assess the stability and spread of the D-estimator outputs.

3. **Extracting Angular Power Spectra**  
   For each simulated map, we compute:
   - $C_\ell^{TT}$, $C_\ell^{EE}$, $C_\ell^{BB}$
   - $C_\ell^{TE}$, $C_\ell^{TB}$, $C_\ell^{EB}$
   using `healpy.anafast`.

4. **Applying D-Estimators**  
   The estimators implemented are:

   - **EB estimator:**
     $D_\ell^{EB}(\beta) = C_\ell^{EB,obs} \cos(4\beta) - \frac{1}{2} \left(C_\ell^{EE,obs} - C_\ell^{BB,obs}\right) \sin(4\beta)$

   - **TB estimator:**
     $D_\ell^{TB}(\beta) = C_\ell^{TB,obs} \cos(2\beta) - C_\ell^{TE,obs} \sin(2\beta)$

5. **Chi-Squared Analysis**  
   For each simulation, a chi-squared statistic is built for each estimator:

   - **EB estimator chi-squared:**
     
     ![chi2_EB](https://quicklatex.com/cache3/c7/ql_b47a51677d24c8fc792739d77b01fcc7_l3.png)
     

   - **TB estimator chi-squared:**
     
     ![chi2_TB](https://quicklatex.com/cache3/62/ql_9433e46330631e5e94c26e78ec703962_l3.png)


   - **Joint (EB+TB) estimator chi-squared:**
  
     ![chi2_joint](https://quicklatex.com/cache3/ed/ql_37a9212a4c7ff9abb18efa968cf0cfed_l3.png)
  
     where the inverse covariance matrix is:
  
     ![inv_cov_joint](https://quicklatex.com/cache3/2f/ql_e4ae3dccd64fea944854e888f933e02f_l3.png)
 
   The value of $\beta$ that minimizes each $\chi^2(\beta)$ is taken as the best-fit birefringence angle for that simulation.

7. **Statistical Evaluation**  
   The best-fit $\beta$ from each simulation is collected. Their distribution is analyzed and compared to the analytical uncertainties derived in the thesis:

   - **EB estimator uncertainty:**

     ![sigma_EB](https://quicklatex.com/cache3/24/ql_bffd835dba55abf4829f19b03c8b6a24_l3.png)

   - **TB estimator uncertainty:**

     ![sigma_TB](https://quicklatex.com/cache3/3f/ql_ba401d580f9703dde360143da1eb623f_l3.png)
  
   - **Joint (EB+TB) estimator uncertainty:**

     ![sigma_joint](https://quicklatex.com/cache3/63/ql_0e706f67eba0ba3cc4291d310b398b63_l3.png)


  These theoretical values are compared to the standard deviation of the $\beta$ values estimated from simulations. The analysis also includes the joint estimator, which is dominated by the EB contribution but    benefits from the inclusion of TB information for completeness.


---

## 📊 Results

Note: The current version of the repository includes a working simulation and analysis pipeline, but the project is still in progress and the implementation is not yet complete. Both the coding and the scientific analysis are ongoing, and further improvements, refinements, and extensions are planned as the work continues. 

---

## 🛠 Tools and Libraries

- `healpy` – for CMB map simulation and power spectrum analysis
- `numpy` – for array operations and numerical computation
- `matplotlib` – for plotting power spectra and histograms
- Planck 2018 fiducial spectra file

---

## Future Work

- Incorporate foreground residuals and instrumental noise
- Apply to masked (cut-sky) simulations for realism
- Extend analysis to Planck CMB polarization data

---

This project is a numerical continuation of my thesis, developed under the supervision of Dr. Alessandro Gruppuso, with the support of Simone Paradiso.
