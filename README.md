# Review terraform plan

Run and cleanup terraform plan output, store it into an output to allow reviewing it
## Inputs
### `terraform-environment`

**Required** Terraform environment, used to load corresponding var file named `<terraform-environment>.tfvars`
into the working directory. Default `"preproduction"`.
### `working-directory`

**Required** Working directory where terraform plan is executed. Default `"."`.

## Example usage


Here

```yaml
- uses: gogaille/review-terraform-plan
  id: terraform-plan
  env:
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
  with:
    terraform-environment: 'preproduction'
    working-directory: 'infrastructure'

- uses: phulsechinmay/rewritable-pr-comment@v0.3
  with:
    message: ${{ steps.terraform-plan.outputs.plan-details }}
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    COMMENT_IDENTIFIER: 'terraform-plan-output'
```
