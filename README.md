# Fine-tuning

The goal of the second part of the school project for the subject ADSDB (Algorithms, Data Structures, and Databases) is to leverage the pipeline developed in the first part to generate training data for fine-tuning an embedding-generation model. For this purpose, we will use the repository created in the previous work as a baseline and continue following a structured workflow, progressing from training data construction to model fine-tuning in layered zones, similar to the approach used earlier.

---

## First Steps

### Working Environment for Notebooks

- Open a terminal and start the Jupyter Notebook framework:
```bash
jupyter notebook
```
- Execute the notebooks in your browser.

---

### Start Docker Containers

Open Docker Desktop and launch the following containers:

#### MinIO
```bash
docker run -d --name minio \
  -p 9000:9000 -p 9001:9001 \
  -e MINIO_ROOT_USER=minioadmin \
  -e MINIO_ROOT_PASSWORD=minioadmin \
  -v C:\minio\data:/data \
  minio/minio server /data --console-address ":9001"
```
- Access the Web UI at [http://127.0.0.1:9001](http://127.0.0.1:9001)

#### ChromaDB
```bash
docker run -d --name chroma \
  -p 8000:8000 \
  -e PERSIST_DIRECTORY=/chroma/chroma \
  -v C:\chromadb\exploitation-zone:/chroma/chroma \
  chromadb/chroma:latest
```
- Although we set a path for ChoromaDB to persistently store embeddings here. It seems like ChromaDB actually stores the embeddings inside the container

---

## Execution Order

### Landing Zone
- `landing_zone.ipynb`  
- `temporal_landing.ipynb`  
- `persistent_landing.ipynb`  

### Formatted Zone
- `formatted_zone.ipynb`  
- `formatted_zone_homogenizer_texts.ipynb`  
- `formatted_zone_homogenizer_images.ipynb` 

### Trusted Zone
- `trusted_zone.ipynb`  
- `trusted_zone_text_quality_processes.ipynb`
- `trusted_zone_image_quality_processes.ipynb`

### Exploitation Zone
- `exploitation_zone_text_embeddings.ipynb`
- `exploitation_zone_image_embeddings.ipynb`
- `exploitation_zone_text_image_embeddings.ipynb`

### Training Data Construction Zone
- `training_data_generation.ipynb`

> Follow this order so that data flows correctly from ingestion to exploitation while maintaining the layered structure.

## Notes

- Each notebook corresponds to a specific stage in the pipeline.

