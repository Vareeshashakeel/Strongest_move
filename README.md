# VID-Trans-ReID camera-agnostic intermediate XCam version

This repo is a stronger version of the camera-removed baseline.

## Main change
It adds **intermediate cross-camera supervised contrastive learning** inside the ViT feature extractor instead of only using losses after the final global branch.

## What changed
- no camera metadata is used as model input
- camera labels are used only to build training positives in the loss
- intermediate transformer tokens from selected blocks are aggregated into sequence-level features
- cross-camera same-ID features are pulled closer with supervised contrastive loss
- sampler prefers multi-camera instances for the same identity inside a batch
- inference remains camera-agnostic

## Default strong setting
- xcam blocks: `5,8`
- xcam weight: `0.15`
- temperature: `0.07`
- same-camera fallback weight: `0.25`

## Train example
```bash
python VID_Trans_ReID.py   --Dataset_name Mars   --model_path /path/to/jx_vit_base_p16_224-80ecf9dd.pth   --batch_size 16   --epochs 40   --eval_every 10   --num_workers 2   --output_dir ./outputs_xcam
```
