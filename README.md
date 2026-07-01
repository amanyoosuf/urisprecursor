# Precursor to my URIS project

# SmartGrid-AI: Predictive Situational Awareness Dashboard

An interactive full-stack grid analytics dashboard designed to simulate and visualize real-time voltage profiles on distribution networks under heavy Electric Vehicle (EV) charging loads. 

This project serves as the foundational data generation pipeline and operational visualization layer for the Undergraduate Research Internship Scheme (URIS) at The Hong Kong Polytechnic University (PolyU), developed in alignment with the Research Centre for Grid Modernisation (RCGM).

My current URIS project has 3 main objectives:

  - Objective 1: To develop and train a Deep Learning model for Dynamic State Estimation (DSE) using
  time-series simulated operational data from a representative distribution feeder (IEEE 33-bus system).
  The model will learn to forecast future voltage profiles from historical measurement sequences,
  establishing baseline forecasting accuracy against a persistence model and a static DNN benchmark.

  - Objective 2: To evaluate the robustness of the proposed DSE model under challenging dynamic grid
    scenarios, specifically measurement loss and bad data injection occurring during time-varying load ramps
    (e.g., EV charging peaks) . The analysis will quantify the model's resilience in low-observability
    conditions where traditional static WLS fails and where forecasting errors could lead to undetected
    violations.

  - Objective 3: To extend the dynamic state estimation framework to predictive situational awareness by
    developing a visualization module that interprets forecasted voltage trajectories, identifies impending
    constraint violations, and issues early warnings (e.g., undervoltage expected in 5 minutes during EV
    peak). This demonstrates practical applicability for proactive real-world grid monitoring.

## Live Demo
Explore the production dashboard here: [Insert Your Live Vercel/Netlify Link Here]

## Core Concept & Research Context
Modern electrical distribution grids face a critical challenge: low observability. Traditional grid monitoring algorithms, such as Weighted Least Squares (WLS) state estimation, rely on high-density physical sensor placement and rigid structural grid models. As Hong Kong accelerates its clean energy transition—introducing volatile, localized loads like high-density EV charging stations—these rigid physics formulas struggle to map or predict grid anomalies when sensor data is lost or intermittent.

The ultimate objective of this URIS project is to transition from static, physics-reliant sight to AI-driven predictive foresight (Predictive Situational Awareness). By utilizing Recurrent Neural Networks (RNNs/LSTMs), the framework aims to learn the complex temporal relationships within sparse measurement data to predict future bus voltages minutes ahead of time.

This repository implements the essential baseline data and visualization architecture for that research roadmap.

## Project Architecture & Data Flow

1. Backend Engine (/backend): Written in Python using the pandapower engine. It initializes a standard IEEE 33-bus radial network and runs a quasi-static time-series power flow over 144 ten-minute intervals (a complete 24-hour cycle). To mimic the localized infrastructure stress of Hong Kong's evening rush hour, it injects a synthetic EV charging spike profile between 6 PM and 10 PM at critical nodes (Bus 15 and Bus 22).

2. Frontend Dashboard (/frontend): A responsive web interface built with React.js and Recharts. It streams the multi-node voltage arrays from the simulation output and monitors them in real-time. It applies built-in safety boundary parameters (< 0.95 p.u.) to instantly flash visual alert notifications, notifying operators of impending undervoltage failures.

## Tech Stack
* Backend: Python 3.x, Pandapower, Pandas, NumPy
* Frontend: React.js (Vite), Recharts, HTML5, CSS3

## Local Setup & Installation

### 1. Execute the Power Flow Simulation
```bash
cd backend
pip install pandapower pandas numpy
python simulation.py
