Here's a nice BASH trick to search all git-files for a string:
Add this to ~/.bash_profile:
```bash
function gg() {
  for f in $( git ls-files $2 ); do
      grep --line-number --no-messages --ignore-case --color \
          $1 $f \
          /dev/null  # https://stackoverflow.com/questions/15432156/display-filename-before-matching-line
  done
```
Example output:

```bash
pi@pPro18 ~/code/2020/ (update-lambda)
> gg aws_storage_bucket_name .
create-env.sh:144:    f3 AWS_STORAGE_BUCKET_NAME \
deploy/kubernetes/yaml-templates/002-django-secrets:10:  aws_storage_bucket_name:  $AWS_STORAGE_BUCKET_NAME
deploy/kubernetes/yaml-templates/env:64:            - name: AWS_STORAGE_BUCKET_NAME
deploy/kubernetes/yaml-templates/env:65:              value: "$AWS_STORAGE_BUCKET_NAME"
leafsheets/models.py:53:from leafsheets_django.settings import LAMBDA_URL, AWS_STORAGE_BUCKET_NAME
leafsheets/models.py:381:            'bucket' : AWS_STORAGE_BUCKET_NAME,
leafsheets_django/settings.py:119:    AWS_STORAGE_BUCKET_NAME = env('AWS_STORAGE_BUCKET_NAME')
leafsheets_django/settings.py:122:    AWS_S3_CUSTOM_DOMAIN = f'{AWS_STORAGE_BUCKET_NAME}.s3.amazonaws.com'
magic.sh:422:    _create_s3_bucket_if_not_exist $AWS_STORAGE_BUCKET_NAME Enabled
table.sh:29:AWS_STORAGE_BUCKET_NAME         :no_entry:️              :no_entry:️              :white_check_mark:              :no_entry:️   # needed in magic.sh (to create bucket), and (to process .docx -> .pdf)
pi@pPro18 ~/code/2020/ (update-lambda)
> gg aws_storage_bucket_name ./create-env.sh 
create-env.sh:144:    f3 AWS_STORAGE_BUCKET_NAME \
```
