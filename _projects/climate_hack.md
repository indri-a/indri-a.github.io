---
layout: page
title: Ohm Sweet Ohm
description: Computer vision app that calculates carbon emissions
img: assets/img/commonhealth.png
importance: 1
category: fun
#giscus_comments: true
---

## Challenge

In November 2024, I participated in an Energy and Climate Hackathon run by MIT. There were 8 challenges presented by different companies and startups, and my team participated in the challenge run by [Planet FWD](https://www.planetfwd.com/). 

Planet FWD is a decarbonization platform that helps companies measure, report, and reduce their carbon footprints across their products. Their challenge was to **"Use computer vision to dynamically infer carbon footprints."** We would be using their brand-new API that took a product's name and mass as input, and output an estimate of that product's CO2 emissions.

[![Challenges](/assets/img/challenges.jpg){:style="width:100%; max-width:800px; height:auto; display:block; margin:0 auto"}](/assets/img/challenges.jpg)

## Picking the computer vision model

Our first decision was to pick what computer vision model to use for our application. I evaluated a number of pre-trained open-source computer vision models including:

- [MobileNetV2](https://www.tensorflow.org/api_docs/python/tf/keras/applications/MobileNetV2)
- [ResNet50](https://huggingface.co/microsoft/resnet-50)
- [YOLOv8](https://github.com/ultralytics/ultralytics/blob/main/docs/en/models/yolov8.md)

Unfortunately, none of the open-source models worked that well with the types of objects we wanted to identify (food):

[![coke can yolov8](/assets/img/coke_yolov8.JPG){:style="width:100%; max-width:800px; height:auto; display:block; margin:0 auto"}](/assets/img/coke_yolov8.JPG)

To correctly identify retail and food objects, we would have to fine-tune the open-source computer vision models with retail data images, and unfortunately we didn't have the time or compute to do so (we only had 24 hours for this hackathon.)

Instead, I decided to cough up $5 to use OpenAI's [GPT-4o-mini](https://openai.com/index/gpt-4o-mini-advancing-cost-efficient-intelligence/) model. It worked really well at both identifying food/retail objects, as well as estimating the mass of the object, both parameters we needed to use Planet FWD's API for estimating carbon emissions.

## Model pipeline

Here was the final model pipeline for our app:

[![Model pipeline](/assets/img/model_pipeline.png){:style="width:100%; max-width:800px; height:auto; display:block; margin:0 auto"}](/assets/img/model_pipeline.png)

## App

Here's the app my team and I managed to finish at 1AM in the morning:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include video.liquid path="assets/video/demo.mp4" class="img-fluid" height="50" controls=true %}
    </div>
</div>

Ultimately we did not win, but we had a lot of fun! 🎉