# Product Brand Module for Odoo

This Odoo module allows you to add and manage brands for your products. Each brand can have an associated image, and you can display brand information directly on product forms.

## Features

- Add and manage product brands
- Assign brands to products
- Display brand images
- Retrieve brand images via URL
- Filter products by brand

## Installation

1. **Clone the repository to your Odoo add-ons directory:**

   ```bash
   git clone https://github.com/yourusername/odoo-product-brand.git
   ```

2. **Update your Odoo configuration file (`odoo.conf`) to include the add-ons directory if not already done:**

   ```ini
   [options]
   addons_path = /path/to/your/odoo/addons,/path/to/your/cloned/repo
   ```

3. **Restart your Odoo server:**

   ```bash
   sudo service odoo restart
   ```

4. **Install the `Product Brand` module via the Odoo Apps interface:**

   - Go to **Apps**.
   - Click on the **Update Apps List** button.
   - Search for `Product Brand`.
   - Click on **Install**.

## Usage

1. **Create a Brand:**

   - Go to **Sales** > **Products** > **Product Brands**.
   - Click on the **Create** button.
   - Fill in the Brand Name, Description, and upload an Image.
   - Click on **Save**.

2. **Assign a Brand to a Product:**

   - Go to **Sales** > **Products** > **Products**.
   - Open a product form.
   - Select the brand in the **Brand** field.
   - Click on **Save**.

3. **View Brand Image:**

   - The brand image can be accessed via the URL:

     ```
     http://your_odoo_server/api/brand/<brand_id>/image
     ```

## API Endpoints

### Get Brand Image

- **URL:** `/api/brand/<brand_id>/image`
- **Method:** `GET`
- **Description:** Retrieve the image for a specific brand by its ID.

## Example Code to Fetch Data

### Fetch All Brands with Images

```typescript
public async getAllBrandsWithImages() {
  const brands = await this.client.call<any>("call", {
    service: "object",
    method: "execute_kw",
    args: [
      ODOO_DB,
      this.uid,
      ODOO_APIKEY,
      "product.brand",
      "search_read",
      [
        [], // Domain to filter records (empty means no filtering)
        ["id", "name", "image_url"], // Fields to retrieve
      ],
    ],
  });
  return brands;
}
```
