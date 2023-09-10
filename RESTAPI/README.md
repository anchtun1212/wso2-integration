# Test project zero

Go to: `Deployed APIs` and copy the URL you want to test

Run: `curl -v GET "URL_TO_RUN in Deployed APIs" -w "\n"`

Example: `curl -v GET "http://localhost:8290/orders" -w "\n"`

Example: `curl -v GET "http://localhost:8290/orders/tunisia" -w "\n"` ==> same default log message

Run: `curl -v GET "http://localhost:8290/orders/month/{currentMonth}" -w "\n"`

Example: `curl -v GET "http://localhost:8290/orders/month/october" -w "\n"`