# python-adaptive-google-places-poi-sampler
A smart, budget-friendly spatial sampling algorithm for high-efficiency POI data retrieval from Google Places API.

## Overview / Background

In urban analytics and smart city research, acquiring high-resolution Point of Interest (POI) data is indispensable. While commercial mapping services like the Google Places API offer comprehensive datasets, their pay-as-you-go pricing models create a significant "budget barrier." 

Existing spatial sampling strategies, such as **fixed grid approaches**, face an inherent methodological trade-off:
* **In sparse suburban areas:** They incur prohibitive costs due to thousands of redundant API calls.
* **In dense urban cores:** They suffer from severe data omission (reduced recall) because they easily exceed the API's maximum return limit (e.g., 20 results per request).

**Our Approach:** To address this dilemma, we reframe the data retrieval process as a *capacity-constrained facility location problem with unknown demand*. This repository provides an **adaptive greedy sampling algorithm** based on the geometric set cover problem. By using the distance to the farthest retrieved POI as the "effective radius," the algorithm dynamically adjusts the search radius and geometrically subtracts fully explored areas. This guarantees a 100% retrieval rate without wasting API requests on empty spaces.

## Key Features

* **Massive Cost Reduction:** Reduces the total number of API calls by **80% to 99%** compared to conventional fixed-grid baselines.
* **100% Data Completeness:** Geometrically guarantees zero data omissions by naturally adapting to any extreme urban density.
* **High Versatility:** While optimized for Google Places API (Nearby Search), the core continuous subtraction algorithm can be easily adapted to other commercial APIs with pagination or return limits.
* **Interactive & Accessible:** The entire algorithm is provided as an easy-to-use Jupyter Notebook, making it simple to visualize sampling boundaries and understand the iterative process.

## Installation
Since the project is provided as a standalone Jupyter Notebook, simply clone the repository and ensure you have the standard geospatial and data science libraries installed.

```bash
git clone [https://github.com/your-username/python-adaptive-google-places-poi-sampler.git](https://github.com/your-username/python-adaptive-google-places-poi-sampler.git)
cd python-adaptive-google-places-poi-sampler
```

**Dependencies:**
You will need the following Python libraries installed in your environment:
`pandas`, `geopandas`, `shapely`, `requests`, `numpy`, `scipy`, `matplotlib`, and `matplotlib-scalebar`.

## Usage / Quick Start
The complete sampling algorithm and visualization tools are contained within `restaurants_google_API_Eng_final.ipynb`. 

1. Open the notebook using Jupyter or Google Colab:
   ```bash
   jupyter notebook restaurants_google_API_Eng_final.ipynb
   ```
2. Insert your valid **Google Places API Key** in the setup cell.
3. Define your target area (Polygon) and desired POI types (e.g., restaurants, cafes).
4. **Run all cells:** The notebook will systematically execute the adaptive sampling, print the progress, dynamically adjust the search radii, and output a clean DataFrame of retrieved POIs without duplicates.
5. The notebook also includes visualization cells to help you verify the sampling strategy geometrically on a map.

## Citation
This tool is based on the research accepted for publication in the ISPRS Annals of the Photogrammetry, Remote Sensing and Spatial Information Sciences (2026). The official publication details (DOI, volume, etc.) will be updated once published.

If you use this tool in your research, please cite our paper as follows for now:
```bibtex
@inproceedings{kikuchi2026adaptive,
  title={Democratizing high-resolution urban data: A cost-effective greedy algorithm for POI retrieval using Google Places API},
  author={Kikuchi, Hozumi; Inoue, Takuo; Nakajima, Hiroki& Koizumi, Hideki},
  booktitle={ISPRS Annals of the Photogrammetry, Remote Sensing and Spatial Information Sciences (Accepted)},
  year={2026},
  note={Accepted for publication}
}
```

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
