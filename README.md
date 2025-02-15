


---
# Huawei Cloud OBS Sync Action

![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Sync--OBS-blue)  
This GitHub Action allows you to easily sync files to **Huawei Cloud OBS** (Object Storage Service) using obsutil. It helps automate the process of transferring/synchronizing files from your repository or build artifacts to OBS in your cloud environment.

## Features

- Automate Syncing files to Huawei Cloud OBS (Object Storage Service) from a GitHub repository.
- Configurable for different environments and storage buckets.
- Supports syncing entire directories or specific files.
- Easily configurable with your Huawei Cloud credentials.
- Uses [`obsutil`](https://support.huaweicloud.com/intl/en-us/utiltg-obs/obs_11_0001.html) for high-performance uploads.

## Prerequisite
Before using this action, make sure you have the following:

- A valid OBS access key and secret key.
- The OBS bucket where you want to sync the files.

## Inputs

| Name          | Description                                                   | Required | Example                                      |
|---------------|---------------------------------------------------------------|----------|----------------------------------------------|
| `accessKey`    | The Access Key ID for your Huawei Cloud OBS account.[`More Info`](https://support.huaweicloud.com/intl/en-us/clientogw-obs/obs_03_0405.html)                              | Yes      | `${{ secrets.ACCESS_KEY }}`                  |
| `secretKey`   | The Secret Key for your Huawei Cloud OBS account. [`More Info`](https://support.huaweicloud.com/intl/en-us/clientogw-obs/obs_03_0405.html)                              | Yes      | `${{ secrets.SECRET_KEY }}`                 |
| `region`    | The region where your OBS bucket is located (e.g., af-south-1). [`More Info`](https://console-intl.huaweicloud.com/apiexplorer/#/endpoint/OBS)                           | Yes      | `af-south-1` |
| `obsBucket`   | The OBS bucket name or path where the files will be synced to.                                              | Yes      | `my-bucket`                     |
| `localPath`   | The local file or folder you want to sync to OBS.             | Yes      | ` dist/ or file to sync`                            |

## Example Usage
Here’s an example of how to use this action in your GitHub workflow:
- The action is triggered on push to the main branch.
- The files in dist/ directory are synced to the specified OBS bucket.

```yaml
name: Sync to Huawei Cloud OBS

on:
  push:
    branches:
      - main

jobs:
  sync-job:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Sync files/folder to Huawei Cloud OBS bucket
        uses: lemrex/Sync-OBS@v1.0.0
        with:
          accessKey: ${{ secrets.ACCESS_KEY }}
          secretKey: ${{ secrets.SECRET_KEY }}
          region:    af-south-1
          obsBucket: your bucket name
          localPath: dist/  # Local directory to sync
```

### Notes
- You can specify any local path (e.g., ./build-artifacts/) for syncing files to your OBS bucket.
- Make sure that the provided region matches the location of your OBS bucket.

## Troubleshooting
- Invalid Credentials: Make sure your OBS access and secret keys are correctly set in GitHub Secrets.
- Sync Issues: Ensure that the OBS bucket and region are correctly specified.
- File Path: Double-check the localPath to ensure it's pointing to the correct folder or file.
- Check the `obsutil` logs in the action's output for additional details.


## License

This action is licensed under the [MIT License](LICENSE).



Feel free to open an issue if you encounter any problems or have feature requests!

---