-- 1. Create `brand` table
CREATE TABLE brand (
    brand_id INT AUTO_INCREMENT PRIMARY KEY,
    brand_name VARCHAR(255) NOT NULL
);

-- 2. Create `product_category` table
CREATE TABLE product_category (
    category_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(255) NOT NULL
);

-- 3. Create `product` table
CREATE TABLE product (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    brand_id INT,
    base_price DECIMAL(10, 2),
    category_id INT,
    FOREIGN KEY (brand_id) REFERENCES brand(brand_id),
    FOREIGN KEY (category_id) REFERENCES product_category(category_id)
);

-- 4. Create `product_image` table
CREATE TABLE product_image (
    image_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT NOT NULL,
    image_url VARCHAR(2083) NOT NULL,
    is_primary BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (product_id) REFERENCES product(product_id)
);

-- 5. Create `color` table
CREATE TABLE color (
    color_id INT AUTO_INCREMENT PRIMARY KEY,
    color_name VARCHAR(50) NOT NULL,
    hex_value VARCHAR(7)
);

-- 6. Create `size_category` table
CREATE TABLE size_category (
    size_category_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(255) NOT NULL
);

-- 7. Create `size_option` table
CREATE TABLE size_option (
    size_id INT AUTO_INCREMENT PRIMARY KEY,
    size_category_id INT NOT NULL,
    size_name VARCHAR(50) NOT NULL,
    FOREIGN KEY (size_category_id) REFERENCES size_category(size_category_id)
);

-- 8. Create `product_variation` table
CREATE TABLE product_variation (
    variation_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT NOT NULL,
    color_id INT,
    size_id INT,
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (color_id) REFERENCES color(color_id),
    FOREIGN KEY (size_id) REFERENCES size_option(size_id)
);

-- 9. Create `product_item` table
CREATE TABLE product_item (
    item_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (product_id) REFERENCES product(product_id)
);

-- 10. Create `attribute_category` table
CREATE TABLE attribute_category (
    category_id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(255) NOT NULL
);

-- 11. Create `attribute_type` table
CREATE TABLE attribute_type (
    type_id INT AUTO_INCREMENT PRIMARY KEY,
    type_name VARCHAR(50) NOT NULL
);

-- 12. Create `product_attribute` table
CREATE TABLE product_attribute (
    attribute_id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT NOT NULL,
    category_id INT NOT NULL,
    type_id INT NOT NULL,
    value VARCHAR(255),
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (category_id) REFERENCES attribute_category(category_id),
    FOREIGN KEY (type_id) REFERENCES attribute_type(type_id)
);






