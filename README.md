## Assign Product Images Using Script

>**🔑 _Key Concept_**: Depending on how your org was set up, you may not need to complete any activities related to CMS or product images at all - especially if you used the sample data load. However, you should make note of this section or 📑 _bookmark it as this question comes up often_.

**🛑 _Before you begin_...**
**1**. **** This code approach is for *non-Enhanced CMS and Sites (Stores) only*. A script to support Enhanced CMS is underway. To be clear, it can be used with these combinations of Stores and CMS as of today (08/03/2023):
   **a**. B2B Aura Store + CMS (non-Enhanced)
   **b**. B2B LWR Store (non-Enhanced) + CMS (non-Enhanced)
**2**. ⚠️ Once Enhanced Sites is activated in an org,  _you will not be able to choose any CMS assets from a non-Enhanced CMS until the Winter release_. It’s also possible that the CDN settings may revert which manifests as a CDN error when activating a new LWR store. You can file a case to restore the CDN settings. The specific scenario is outlined in the prior course’s [Activity: Store Settings and Administration Options: B2B Commerce: Deploying the Storefront](https://salesforce.quip.com/MzEAAVbEd9gI#QEBACA8G7j7).
**3**. This script depends on you having previously completed an action such as that outlined in [Load Unstructured Content for CMS Media](https://salesforce.quip.com/7IQzA6BiLA08#temp:C:UUU24f37614a2b84873bc2f8fa0e). The content assets must be present in the org’s CMS before they can be associated to the products.
**4.** Lastly, this script uses an association of SKU to link the images and products when that may not be appropriate in all cases. Per the comment at top of file, Product Code may be a better option.


The script below is example code for how you can assign previously uploaded images to products. The [Product Import GUI or Dataloader](https://help.salesforce.com/s/articleView?id=sf.comm_data_import.htm&type=5) may be able to accomplish the same end if all relationships are adequately preserved, but sometimes scripts are just easier to work with. This particular one fits a niche use case *when the CMS assets exist in the org, but are not yet associated with products*. A [REST API](https://developer.salesforce.com/docs/atlas.en-us.chatterapi.meta/chatterapi/connect_resources_commerce_import_product.htm) which backs the CSV import process is also available. If using the Connect API route is still desirable, here is some general pseudo-code guidance:
 
1. Get the product (ConnectAPI.ProductDetail)
2. For that product, get its product media group (ConnectAPI.ProductMediaGroup)
3. For those groups, get their media items (ConnectAPI.ProductMedia)
4. Iterate to get the Electronic Media Ids
5. With it, get the Managed Content Version Collection (ConnectApi.ManagedContentMediaSourceNodeValue)
6. From that, get the URL

The following example class can be created in an org from Setup and then executed using the Execute Anonymous Window in Developer Console or called other ways such as with an IDE like VS Code. A few points before running the script:

* You must have already uploaded your JSON file with images. See the section [Load Unstructured Content for CMS Media](https://salesforce.quip.com/7IQzA6BiLA08#temp:C:UUU24f37614a2b84873bc2f8fa0e)
* Don’t forget to set the COMMUNITY_NAME constant to the correct value for your Store before creating the class
* If you’ve been following the guides to the letter, COMMUNITY_NAME should be something like one of these:
    * **Capricorn B2B Store**
 
# To execute the script, run:
B2BProductMediaImporterPlcExample.createProductMedia();
