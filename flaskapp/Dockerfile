FROM python:3.9-slim-bullseye

# Setup apt and pip
RUN apt update && apt upgrade -y
RUN apt install nano
RUN python -m pip install --upgrade pip

# Create nonroot user
RUN useradd nonroot
RUN mkdir /home/app
RUN chown -R nonroot:nonroot /home/app

# Setup log files
RUN mkdir -p /var/log/flaskapp
RUN touch /var/log/flaskapp.err.log /var/log/flaskapp.out.log
RUN chown -R nonroot:nonroot /var/log/flaskapp
WORKDIR /home/app

COPY --chown=nonroot:nonroot . .
RUN export FLASK_APP=app.py

RUN pip install -r requirements.txt

USER nonroot
CMD ["python", "app.py"]