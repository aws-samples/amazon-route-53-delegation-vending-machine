## Amazon Route 53 Delegation Vending Machine

Setting up a domain in Amazon Route 53 for use with an organization is an effective way to consolidate resources under a unified "namespace".  In this process, creating subdomain zones and delegating them to individual teams helps compartmentalize usage of the overall domain namespace to those relevant teams, limiting risk of collisions should any team decide to utilize the same namespace for their purposes.  However, creating and maintaining the subdomain zone delegation with the parent zone(s) can become an arduous task with many teams or anything else that elicits the need for subdomain zone creation.  Natively, this is a manual process of creating the relevant subdomain zone and taking note of the nameservers (delegation set) assigned to it and creating an NS record in the parent zone whose value is that delegation set.  This solution aims to automate this process using AWS Service Catalog to create a self-service product that can be deployed as needed and which will manage the needed zone and record creation.

## Usage

1. Clone the repository and upload the files found in the `templates/` directory to an S3 bucket.  Ensure that this bucket has a policy that allows read access for the AWS account you identify as the location of the Amazon Route 53 Delegation Vending Machine.  This account should be the account that contains the parent Route 53 hosted zone that will be delegating to the subdomain hosted zones created by the product.

2. Once the files have been uploaded to an S3 bucket, launch the CloudFormation template "route53_delegation_vending_machine.baseline.template.yml" in the administrator account.  You may use a local copy of the template or reference the same template previously uploaded to an S3 bucket.

3. After launching the baseline template, locate the "Route 53 Delegation Vending Machine" product now available via Service Catalog in the account identified as containing the Amazon Route 53 Delegation Vending Machine.  Providing the relevant subdomain AWS account ID, parent Route 53 hosted zone ID, and subdomain hosted zone name, launch the product.

4. Upon launching the Service Catalog product, view the parent Route 53 hosted zone in the Console (https://us-east-1.console.aws.amazon.com/route53/v2/hostedzones) and locate the delegation record (the type will be "NS") by searching for the subdomain hosted zone name used in the previous step.  Validate that the nameserver values in this record are the same as the delegation set for the subdomain hosted zone that has been created in the subdomain AWS account, also provided in the previous step.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

