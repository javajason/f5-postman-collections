# f5-postman-collections

## BIG-IQ Discovery and Import - PostMan Collection
The "BIG-IQ Discovery and Import - PostMan Collection" works with the "Agility 2022 Security Automation with BIG-IQ (version 6)" blueprint on UDF. (See https://udf.f5.com/b/cce0160b-34b1-423b-84b5-82f77c7cd8b4#documentation)

Import this collection into Postman on the Windows Jump Host from the lab. (Hint: the easiest way to do this may be to create a new text file, locally, on the Windows Jump Host, paste the JSON from this file into it, and import from the local file.)

Once the collection has been imported, create the following variables in the "Security Automation Lab" environment:
- REST_ID
- MACHINE_ID
- X-F5-Auth-Token
- F5-Auth-Token-Expiry

You do not need to assign them values, as the "Tests" scripts from the HTTP requests will populate them as you run each request.
The variables, BIGIP_MGMT_IP, BIGIP_ADMIN_USERNAME, BIGIP_ADMIN_PASSWORD, BIGIQ_MGMT_IP, BIGIQ_ADMIN_USERNAME, and BIGIQ_ADMIN_PASSWORD, should already exist in the "Security Automation Lab" Postman environment.

Notes on Running the Collection:
- When running through the requests in the collection, the "Status of" requests may need to be run more than once, since each task may take several seconds (or longer) to complete. Be sure the "Status of" requests shows a status of "FINISHED" before proceeding to the next POST request.
- This collection is only designed to trust, discover, and import one device at a time, and only imports the LTM module. It *should* work with a larger group of devices and with multiple modules, but this hasn't been tested for this collection.

The documents used in creating this collection were the following:
- This blog provides an overview of the process, though there were some steps and pitfalls I needed to figure out for myself:
  https://community.f5.com/t5/technical-articles/big-iq-central-management-api-automation-and-programmability/ta-p/273712
- The API Reference for APIs used in this collection:
  https://clouddocs.f5.com/products/big-iq/mgmt-api/v0.0/ApiReferences/bigiq_public_api_ref/r_public_api_references.html
- The sequence I used, along with the related docs, is the following:
  - Establish Device Trust: https://clouddocs.f5.com/products/big-iq/mgmt-api/v0.0/HowToSamples/bigiq_public_api_wf/t_establish_trust.html
  - MachineId Resolver: https://clouddocs.f5.com/products/big-iq/mgmt-api/v0.0/ApiReferences/bigiq_public_api_ref/r_machineid_resolver.html
  - Device Discover LTM: https://clouddocs.f5.com/products/big-iq/mgmt-api/v0.0/HowToSamples/bigiq_public_api_wf/t_discover_ltm.html
  - Device Import: https://clouddocs.f5.com/products/big-iq/mgmt-api/v0.0/ApiReferences/bigiq_public_api_ref/r_device-import.html
    (Note: for the import, I had more success using this URL to POST my request to: https://[BIG-IQ IP]/mgmt/cm/adc-core/tasks/declare-mgmt-authority)
