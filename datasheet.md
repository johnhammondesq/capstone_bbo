Datasheet for the Black Box Optimization (BBO) Capstone Dataset
1. Motivation
•	Why was the dataset created?
This dataset was created to evaluate, benchmark, and analyze the performance of surrogate-based optimization methods—specifically Gaussian Process regression coupled with Upper Confidence Bound and L-BFGS-B acquisition optimization—across complex, continuous numerical surfaces.
•	What tasks does it support?
It supports research into:
1.	High-dimensional black-box function optimization (F1 through F8).
2.	The integration of LLM reasoning, structured decoding, and tool-use orchestration with classical surrogate modeling.
3.	Spatial exploration versus exploitation trade-offs under finite evaluation budgets (n = 24 to 49).
•	Who created the dataset?
The dataset was iteratively generated during the Black Box Optimization capstone research campaign.
2. Composition
•	What does the dataset contain?
It contains evaluation tuples representing input candidate vectors and their corresponding scalar objective scores across eight distinct test functions (F1 through F8):
o	F1 to F3: Low-dimensional benchmark functions (2D to 3D, such as drug side-effect minimization in F3).
o	F4 to F6: Mid-dimensional surfaces (4D to 5D, such as warehouse placement approximation in F4, chemical process yield in F5, and cake recipe optimization in F6).
o	F7 to F8: High-dimensional hyperparameter tuning surfaces (6D to 8D, such as ML model performance in F7 and validation accuracy in F8).
•	What is the size and format?
o	Format: Textual float-vector notation formatted as fN(x1, x2, ..., xd) = score alongside corresponding dash-delimited coordinate candidate strings (x1-x2-...-xd).
o	Size: Compact sequence logs ranging from n = 24 evaluations (F3) to n = 49 evaluations (F8).
•	Are there any gaps or missing values?
Yes. Extremely low negative evaluation scores falling below background noise thresholds (such as values near 10 to the power of -180) were systematically pruned or excluded to prevent Gaussian Process length-scale distortion. Furthermore, hypervolume coverage is densely clustered near local maxima, leaving significant interior regions of higher dimensions (6D to 8D) unobserved.
3. Collection Process
•	How were the candidate queries generated?
Queries were generated through a hybrid iterative process:
1.	Surrogate Fitting: Fitting an anisotropic Matern 5/2 Gaussian Process kernel with a white noise component to all active historical points.
2.	Acquisition Optimization: Running multi-start L-BFGS-B gradient steps on the GP-UCB acquisition surface (with beta values between 0.8 and 1.5) initiated from top historical evaluation clusters.
3.	Low-Temperature Decoding: Exporting precise candidate vectors using low sampling temperatures (0.0 to 0.2) and strict formatting constraints (x1-x2-...-xn).
•	What strategy was used?
An adaptive exploration-exploitation strategy using Bayesian Optimization (GP-UCB) focused on identifying and refining strong local basins of attraction and domain boundaries.
•	Over what timeframe was it collected?
The dataset was constructed sequentially over an iterative multi-week BBO campaign.
4. Preprocessing and Uses
•	Has any preprocessing or transformation been applied?
o	Range Normalization: All input feature spaces were mapped and bounded within the continuous unit hypercube [0, 1] to the power of d.
o	Noise Floor Filtering: Numerical noise floor entries were excluded prior to fitting surrogate kernels.
o	Maximization Frame: Functions originally designed for minimization (such as F3 and F6) were mathematically transformed into maximization objectives by negating scores or targeting zero bounds.
•	What are the intended uses?
Benchmarking surrogate-based optimization algorithms, studying active learning dynamics in small-sample regimes (N less than 50), and validating hybrid LLM-algorithmic orchestration workflows.
•	What are inappropriate uses?
This dataset should not be used as a representative global distribution of the search domain due to heavy exploitation sampling bias. It is also unsuitable for non-convex global optimization benchmarks that require uniform spatial density.
5. Distribution and Maintenance
•	Where is the dataset available?
The complete evaluation trajectories are recorded in the capstone campaign context logs and code execution artifacts.
•	Who maintains the dataset?
Maintained by the capstone project researcher.
•	What are the terms of use?
Open for academic, research, and technical validation purposes related to black-box optimization and surrogate modeling coursework.

