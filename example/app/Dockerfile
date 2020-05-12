FROM python:3.5

LABEL challenge="covid19"
LABEL ranked_features="cough, body temperature,hematocrit,diastolic blood pressure,systolic blood pressure"
LABEL references="https://www.medrxiv.org/content/10.1101/2020.03.19.20039099v1"
LABEL description="COVID diagnosis baseline prediction"
# Install dependencies
RUN pip install pandas \
  numpy \
  sklearn \
  datetime

# Move to the app folder
RUN mkdir /app
WORKDIR /app

# Copy our python program for training and inference
COPY ./infer.py .


# Copy Bash scripts expected by the IT infrastructure of the EHR DREAM Challenge

COPY ./infer.sh .

# Add executable permission to Bash scripts
RUN chmod +x infer.sh
