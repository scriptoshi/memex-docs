# s3 Storage

### Overview

While our application supports local file storage, we strongly recommend using S3-compatible storage for file uploads (especially logos and images) for several benefits:

* Improved website performance through CDN delivery
* Enhanced security by preventing PHP file execution exploits
* Better scalability and reliability
* Reduced server storage load

### Supported S3 Providers

You can use any S3-compatible storage service, including:

* Linode Object Storage
* DigitalOcean Spaces
* Amazon S3

### Configuration Steps

#### 1. Environment Variables

Add the following credentials to your `.env` file:

```basic
# S3 Storage Credentials
DO_SPACES_KEY=your_access_key
DO_SPACES_SECRET=your_secret_key
DO_SPACES_ENDPOINT=https://eu-central-1.linodeobjects.com
DO_SPACES_REGION=eu-central-1
DO_SPACES_BUCKET=your-bucket-name
DO_SPACES_CDN=https://your-cdn-domain.com/

# Storage Configuration
PROFILE_PHOTO_DISK=do
FILESYSTEM_DISK=do
```

#### 2. Storage Provider Settings

**For Linode Object Storage:**

* Endpoint: Use the appropriate regional endpoint (e.g., `eu-central-1.linodeobjects.com` for Frankfurt)
* Bucket Name: Must match your custom domain name if using one
* Example Region: `eu-central-1` (Frankfurt, DE)

**For DigitalOcean Spaces:**

* Bucket Name: Can be any valid name
* No domain name matching requirement

#### 3. CDN Configuration

If you've configured a custom domain for your bucket:

1. Set `DO_SPACES_CDN` to your custom domain URL (including `https://` and trailing slash)
2. Ensure your DNS records are properly configured
3. Wait for DNS propagation (usually 24-48 hours)

### Important Notes

* The `DO_` prefix in environment variables is historical and works for any S3-compatible service
* Storage options:
  * `public`: Local server storage
  * `aws`: Amazon S3 configuration
  * `do`: Any S3-compatible service (Linode, DigitalOcean, etc.)
* When using Linode, your bucket name must match your custom domain
* For other providers like DigitalOcean, bucket naming is more flexible

### Troubleshooting

If files aren't uploading:

1. Verify your credentials are correct
2. Check bucket permissions
3. Ensure the endpoint URL matches your region
4. Confirm CORS settings if accessing from different domains

For security purposes, always use environment variables and never commit credentials to version control.
