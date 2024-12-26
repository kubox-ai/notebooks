# Use the Jupyter minimal-notebook image as the base image
FROM quay.io/jupyter/minimal-notebook:python-3.11

# Set the working directory inside the container
WORKDIR /home/jovyan/work

# Install required packages
RUN pip install uv
COPY requirements.txt /home/jovyan/work/requirements.txt
RUN uv pip install --no-cache-dir --system -r /home/jovyan/work/requirements.txt

# Copy sample notebooks from the local working directory to the container
COPY GettingStarted.ipynb Nyc-Taxi.ipynb /home/jovyan/work

# Ensure the ownership of the copied files matches the jovyan user
USER root
RUN chown -R jovyan:users /home/jovyan/work
USER jovyan

# Expose the default Jupyter port
EXPOSE 8888

# Start JupyterLab by default
CMD ["start-notebook.sh", "--NotebookApp.token=''"]