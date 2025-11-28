# WildAlert – Early Detection of Forest Fires Using AI and Crowdsourced Phone Photos

Final project for the Building AI course

## Summary
WildAlert is a mobile + web app that lets anyone take a photo of smoke in a forest or rural area. An AI model instantly analyses the image and, if it detects wildfire-like smoke, automatically alerts local authorities and nearby residents – minutes or hours before traditional satellite systems notice the fire. The goal: reduce response time and save lives, homes, and forests.

## Background
Every year, wildfires destroy millions of hectares and cost billions of euros (e.g., 2022–2024 fires in Europe, California, Australia, Amazon). Satellite-based detection often has a 20–60 minute delay and struggles with small or obscured fires under cloud cover. Meanwhile, hikers, farmers, and locals are often the first to see smoke – but they don’t always know whether or whom to call.

Personal motivation: I live close to a large forest that burned in 2023. The fire was reported 45 minutes after the first smoke was visible. I believe AI + the phones already in everyone’s pocket can close that gap.

## How is it used?
1. A hiker sees distant smoke → opens WildAlert app → takes a photo.
2. Photo is sent to the cloud; a computer-vision model decides “wildfire smoke / not smoke” in < 3 seconds.
3. If confidence > 90 %, the app automatically:
   - sends exact GPS coordinates + photo to regional fire services
   - pushes alerts to all users within 20 km
   - posts the alert on a public live map
4. Firefighters get the report while the fire is still small and easy to contain.

Users: hikers, campers, farmers, drone hobbyists, rural residents.  
Non-tech users only need to press one big “Send photo” button.

![Wildfire Smoke Detection Example](https://upload.wikimedia.org/wikipedia/commons/8/8e/Parts_of_the_August_Complex_and_Zogg_Fire_peeking_through_the_smoke_-_September_29th%2C_2020_%2850401114186%29.jpg)  
*Example of early wildfire smoke plumes (August Complex and Zogg Fire, 2020). This is what the app would analyze from a user photo.*

![Forest Fire Close-Up](https://upload.wikimedia.org/wikipedia/commons/2/2c/Photography_of_forest_fire.jpg)  
*Close-up of forest fire with visible smoke – ideal for AI training data (CC BY-SA 4.0).*

## Data sources and AI methods
- Training data:
  - Open wildfire smoke datasets (HPWREN, FLAME, custom-labeled satellite imagery)
  - 50 000+ crowdsourced photos of smoke vs. fog/clouds/bbq (I plan to run a small labeling campaign with scouts and hiking groups)
- Model: lightweight CNN (MobileNetV3 or EfficientNet-B0) → runs fast even on cheap cloud instances and can later be exported to phones for offline use.
- Bonus: add geolocation + time-of-day + wind data from public weather APIs to reduce false positives.


## Challenges
- False positives (fog, steam, dust, barbecue smoke)
- Privacy: photos may accidentally contain people or houses
- Bias: model might perform worse in regions/countries not represented in training data
- Legal: automatic alerts must not overload emergency lines → need official partnerships
- Does NOT replace professional firefighters or satellite monitoring – only complements them.

## What next?
1. Partner with national parks and fire services in 2–3 pilot countries (Finland, Portugal, Greece, California…)
2. Add drone integration and fixed cheap cameras on watchtowers
3. Train a multimodal model that also analyses short video clips + wind direction
4. Create an open dataset of labeled smoke images so the whole research community can improve detection
5. Expand to early flood detection using the same “crowd + AI” principle

Needed help: wildfire domain experts, mobile developers, contacts at fire brigades, funding for cloud inference costs.

## Acknowledgments
- Inspiration from the SmokeSense project (NASA) and the PanoAI camera system
- Base model architecture and training tricks: Google’s “EfficientDet” paper and Teachable Machine export examples
- Open wildfire imagery: HPWREN archive (University of California San Diego)
- Demo space: [ViT-Forest-Fire-Detection by EdoWhite](https://huggingface.co/spaces/EdoWhite/ViT-Forest-Fire-Detection) (MIT License)
- Images: 
  - [Parts of the August Complex and Zogg Fire peeking through the smoke - September 29th, 2020](https://commons.wikimedia.org/wiki/File:Parts_of_the_August_Complex_and_Zogg_Fire_peeking_through_the_smoke_-_September_29th,_2020_(50401114186).jpg) (Public Domain, U.S. Government work)
  - [Photography of forest fire](https://commons.wikimedia.org/wiki/File:Photography_of_forest_fire.jpg) (CC BY-SA 4.0)

Building AI course project – University of Helsinki & Reaktor 2025
