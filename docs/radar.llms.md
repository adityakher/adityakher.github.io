# Multistatic Radar Detection Performance Model

*Status: in progress, last updated 5/10/2026*

This project develops a Python framework for evaluating radar sensor performance against small uncrewed aerial systems (UAS), emphasizing the geometric advantages of multistatic (distributed) configurations over monostatic baselines. The framework implements monostatic and bistatic radar range equations, Shnidman’s detection probability model with Swerling target fluctuation, and an aspect-dependent target radar cross-section model built from composite canonical scatterers and calibrated to published Ku-band small-quadcopter measurements. Outputs include 2D probability-of-detection contours quantifying performance differences between a single monostatic radar and an N-node distributed configuration against low-RCS aspect-dependent targets. The study is motivated by the operational importance of counter-UAS radar and the intuition that geometric diversity in distributed sensor networks provides detection coverage that monostatic systems cannot match, particularly against targets with strong forward-aspect RCS suppression.

### Motivation

Small commercial [UAS](https://en.wikipedia.org/wiki/Unmanned_aerial_vehicle) pose an asymmetric challenge for [radar](https://en.wikipedia.org/wiki/Radar) surveillance: their [RCS](https://en.wikipedia.org/wiki/Radar_cross_section) is low, strongly aspect-dependent, and concentrated in particular directions where monostatic systems are weakest (forward aspect). Distributed (multistatic) radar architectures address this through geometric diversity–different [transmitter](https://en.wikipedia.org/wiki/Transmitter)-[receiver](https://en.wikipedia.org/wiki/Radio_receiver) pairs view the target from different aspects simultaneously, exploiting [bistatic](https://en.wikipedia.org/wiki/Bistatic_radar) RCS behaviors (including forward-scatter enhancement) that monostatic systems can’t access. This project develops a Python framework for quantifying that geometric advantage in detection performance.

### Approach

We integrate three components: (1) a calibrated aspect-dependent UAS RCS model built from composite canonical scatterers (sphere, plate, cylinder primitives) in the [physical optics](https://en.wikipedia.org/wiki/Physical_optics) regime, anchored to published [Ku-band](https://en.wikipedia.org/wiki/Ku_band) measurements of a small commercial [quadcopter](https://en.wikipedia.org/wiki/Quadcopter); (2) the standard radar range equation in monostatic and bistatic forms; (3) Shnidman’s equation[^1] for [fluctuating-target](https://en.wikipedia.org/wiki/Fluctuation_loss) detection probability under Swerling 1 statistics (the appropriate model for small UAS), inverted numerically for \\P_d\\ contour evaluation.

Bistatic RCS[^2] is handled by the monostatic-bistatic equivalence theorem for general bistatic angles, evaluating the monostatic RCS at the bisector aspect. The forward-scatter regime (\\\beta \approx 180\degree\\) is treated separately using \\\sigma\_{FS} \approx 4\pi A^2/\lambda^2\\–a direct application of [Babinet’s principle](https://en.wikipedia.org/wiki/Babinet%27s_principle) to the projected target area. Non-coherent fusion across pairs is implemented by summing linear [SNRs](https://en.wikipedia.org/wiki/Signal-to-noise_ratio) (the high-SNR limit of the [non-central chi-squared](https://en.wikipedia.org/wiki/Noncentral_chi-squared_distribution) detection statistic), justified by the fact that summed independent chi-squared variables yield combined non-centrality \\\lambda = 2\sum{\text{SNR}\_i}\\.

## Footnotes

[^1]: D. A. Shnidman, “Determination of required SNR values \[radar detection\],” in *IEEE Transactions on Aerospace and Electronic Systems*, vol. 38, no. 3, pp. 1059-1064, July 2002, [doi: 10.1109/TAES.2002.1039422](https://doi.org/10.1109/TAES.2002.1039422).

[^2]: M. I. Skolnik, *Introduction to Radar Systems*, 2nd ed. New York: McGraw-Hill, 1980.
