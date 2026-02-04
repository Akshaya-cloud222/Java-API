 (cd "$(git rev-parse --show-toplevel)" && git apply --3way <<'EOF' 
diff --git a/README.md b/README.md
new file mode 100644
index 0000000000000000000000000000000000000000..44f5fcc3ccda4b3fd4e007e655e0d8469021b236
--- /dev/null
+++ b/README.md
@@ -0,0 +1,71 @@
+# Item API (Spring Boot)
+
+A simple Java Spring Boot REST API for managing a small in-memory catalog (think ecommerce or streaming items).
+
+## Requirements
+- Java 17+
+- Maven 3.9+
+
+## Run locally
+```bash
+mvn spring-boot:run
+```
+The API will start at `http://localhost:8080`.
+
+## API Endpoints
+### Add a new item
+`POST /items`
+
+Request body:
+```json
+{
+  "name": "Wireless Mouse",
+  "description": "Ergonomic mouse with USB-C receiver",
+  "price": 24.99,
+  "category": "Accessories"
+}
+```
+
+Response: `201 Created`
+```json
+{
+  "id": 1,
+  "name": "Wireless Mouse",
+  "description": "Ergonomic mouse with USB-C receiver",
+  "price": 24.99,
+  "category": "Accessories"
+}
+```
+
+Validation:
+- `name`, `description`, and `category` are required (non-blank)
+- `price` is required and must be `>= 0`
+
+### Get a single item by ID
+`GET /items/{id}`
+
+Response: `200 OK`
+```json
+{
+  "id": 1,
+  "name": "Wireless Mouse",
+  "description": "Ergonomic mouse with USB-C receiver",
+  "price": 24.99,
+  "category": "Accessories"
+}
+```
+
+If the item does not exist, the API returns `404 Not Found`.
+
+## Notes
+- Data is stored in-memory using an `ArrayList`, so it resets on application restart.
+
+## Hosting / Demo
+I cannot deploy to external hosting providers from this environment. To host the app yourself, build a jar with:
+```bash
+mvn clean package
+```
+Then deploy `target/item-api-0.0.1-SNAPSHOT.jar` to a platform like Render, Railway, or a VM and run:
+```bash
+java -jar target/item-api-0.0.1-SNAPSHOT.jar
+```
 
EOF
)
