# Single Shot Detector Lite
[SSD Lite](https://arxiv.org/abs/1512.02325) high performance general object detection.

## Installing SSD Lite
Add the following items to your Unity project's `Packages/manifest.json`:
```json
{
  "scopedRegistries": [
    {
      "name": "NatML",
      "url": "https://registry.npmjs.com",
      "scopes": ["ai.natml"]
    }
  ],
  "dependencies": {
    "ai.natml.vision.ssd-lite": "1.0.0"
  }
}
```

## Detecting Objects in an Image
First, create the SSD Lite predictor:
```csharp
// Fetch the model data from NatML Hub
var modelData = await MLModelData.FromHub("@natsuite/ssd-lite");
// Deserialize the model
var model = modelData.Deserialize();
// Create the SSD Lite predictor
var predictor = new SSDLitePredictor(model, modelData.labels);
```

Then detect objects in the image:
```csharp
// Create image feature
Texture2D image = ...;
var imageFeature = new MLImageFeature(image); // This also accepts a `Color32[]` or `byte[]`
(imageFeature.mean, imageFeature.std) = modelData.normalization;
imageFeature.aspectMode = modelData.aspectMode;
// Detect objects
(Rect rect, string label, float score)[] detections = predictor.Predict(imageFeature);
```

> The detection rects are provided in normalized coordinates in range `[0.0, 1.0]`. The score is also normalized in range `[0.0, 1.0]`.
___

## Requirements
- Unity 2021.2+

## Quick Tips
- Join the [NatML community on Discord](https://hub.natml.ai/community).
- Discover more ML models on [NatML Hub](https://hub.natml.ai).
- See the [NatML documentation](https://docs.natml.ai/unity).
- Discuss [NatML on Unity Forums](https://forum.unity.com/threads/open-beta-natml-machine-learning-runtime.1109339/).
- Contact us at [hi@natml.ai](mailto:hi@natml.ai).

Thank you very much!