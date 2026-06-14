# Use a minimal base image with Python 3.9 installed
FROM python:3.9

# Create a non-root user and set its home directory
RUN useradd -m -u 1000 user
USER user
ENV HOME=/home/user
# Append to the existing PATH to ensure system binaries and python paths are included
ENV PATH=$HOME/.local/bin:$PATH

# Set the working directory to the app's location within the user's home
# This will be /home/user/app
WORKDIR $HOME/app

# Copy the entire 'tourism_project_updated' folder from the build context
# into the user's app directory, and set user as owner.
# Assuming 'tourism_project_updated' is at the root of the GitHub repo.
COPY --chown=user tourism_project_updated $HOME/app

# Now, install dependencies as the 'user'.
# The requirements.txt file will be at $HOME/app/tourism_project_updated/requirements.txt
RUN pip3 install --no-cache-dir -r $HOME/app/tourism_project_updated/requirements.txt

# Define the command to run the Streamlit app
CMD ["streamlit", "run", "tourism_project_updated/deployment/app.py", "--server.port=8501", "--server.address=0.0.0.0", "--server.enableXsrfProtection=false"]
