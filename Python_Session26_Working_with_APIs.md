# Session 26 — Working with APIs
## Module 6: Automation & Capstone Project | Professional Python Programming Certification
### Duration: 1 Hour | Type: Theory + Hands-On | Hands-On: Fetch and Process Data from Web APIs

---

## Learning Objectives
By the end of this session, you will be able to:
1. Understand what APIs are and how they work
2. Make HTTP requests using the `requests` library
3. Parse and process JSON responses
4. Handle API errors and status codes
5. Work with public APIs for real-world data

---

## 26.1 What is an API?

**API** = Application Programming Interface — a set of rules that allows one software application to communicate with another.

### Real-World Analogy

| Concept | Restaurant Analogy |
|---------|-------------------|
| **You** (Client) | The customer |
| **API** | The waiter |
| **Server** | The kitchen |
| **Request** | Your order |
| **Response** | The food delivered |

### How Web APIs Work

```
Client (Python)          Server (API)
     │                        │
     │── HTTP Request ──────▶│
     │   (GET /weather)       │
     │                        │── Process
     │                        │── Query database
     │◀── HTTP Response ─────│
     │   (JSON data)          │
```

### Types of APIs

| Type | Description | Example |
|------|-------------|---------|
| **REST API** | Most common — uses HTTP methods | GitHub API, Weather API |
| **GraphQL** | Query specific data you need | GitHub GraphQL API |
| **SOAP** | XML-based, enterprise | Legacy banking systems |
| **WebSocket** | Real-time, bidirectional | Chat apps, live data |

---

## 26.2 HTTP Methods

| Method | Purpose | Example |
|--------|---------|---------|
| **GET** | Retrieve data | Get weather, list users |
| **POST** | Create/send data | Submit form, create user |
| **PUT** | Update (replace) data | Update entire user profile |
| **PATCH** | Update (partial) data | Update just the email |
| **DELETE** | Remove data | Delete a user |

### HTTP Status Codes

| Code | Meaning | Category |
|------|---------|----------|
| **200** | OK — Success | ✅ Success |
| **201** | Created | ✅ Success |
| **204** | No Content | ✅ Success |
| **301** | Moved Permanently | 🔄 Redirect |
| **400** | Bad Request | ❌ Client Error |
| **401** | Unauthorized (no/bad auth) | ❌ Client Error |
| **403** | Forbidden (no permission) | ❌ Client Error |
| **404** | Not Found | ❌ Client Error |
| **429** | Too Many Requests (rate limit) | ❌ Client Error |
| **500** | Internal Server Error | ❌ Server Error |
| **503** | Service Unavailable | ❌ Server Error |

---

## 26.3 The `requests` Library

### Installation

```bash
pip install requests
```

### Making a GET Request

```python
import requests

# Simple GET request
response = requests.get("https://api.github.com")

# Response object properties
print(response.status_code)    # 200
print(response.ok)             # True (status < 400)
print(response.headers)        # Response headers dict
print(response.text)           # Raw text response
print(response.json())         # Parse JSON → Python dict
print(response.url)            # Final URL (after redirects)
print(response.elapsed)        # Time taken
```

### GET with Parameters

```python
import requests

# Query parameters
params = {
    "q": "Python programming",
    "sort": "stars",
    "order": "desc",
    "per_page": 5,
}

response = requests.get("https://api.github.com/search/repositories", params=params)

if response.ok:
    data = response.json()
    print(f"Total results: {data['total_count']}")
    for repo in data["items"]:
        print(f"  ★ {repo['stargazers_count']:>6} | {repo['full_name']}")
```

### GET with Headers

```python
# Custom headers (e.g., API key, content type)
headers = {
    "Accept": "application/json",
    "User-Agent": "Python-App/1.0",
    "Authorization": "Bearer YOUR_API_KEY"
}

response = requests.get("https://api.example.com/data", headers=headers)
```

---

## 26.4 Making POST Requests

```python
import requests

# POST with JSON body
data = {
    "title": "New Post",
    "body": "This is the content.",
    "userId": 1
}

response = requests.post(
    "https://jsonplaceholder.typicode.com/posts",
    json=data   # Automatically serializes to JSON and sets Content-Type
)

if response.status_code == 201:
    result = response.json()
    print(f"Created post with ID: {result['id']}")
```

### POST with Form Data

```python
# For form-encoded data (like HTML forms)
form_data = {
    "username": "alice",
    "password": "secret123"
}

response = requests.post("https://example.com/login", data=form_data)
```

---

## 26.5 Handling API Responses

### Checking Status Codes

```python
import requests

response = requests.get("https://api.github.com/users/octocat")

if response.status_code == 200:
    data = response.json()
    print(f"User: {data['login']}")
    print(f"Name: {data['name']}")
    print(f"Repos: {data['public_repos']}")
elif response.status_code == 404:
    print("User not found!")
elif response.status_code == 403:
    print("Rate limit exceeded. Try later.")
else:
    print(f"Error: {response.status_code}")
```

### Using raise_for_status()

```python
try:
    response = requests.get("https://api.example.com/data")
    response.raise_for_status()  # Raises HTTPError for 4xx/5xx
    data = response.json()
except requests.exceptions.HTTPError as e:
    print(f"HTTP Error: {e}")
except requests.exceptions.ConnectionError:
    print("Connection failed. Check your internet.")
except requests.exceptions.Timeout:
    print("Request timed out.")
except requests.exceptions.RequestException as e:
    print(f"Request failed: {e}")
```

### Timeout

```python
# Set timeout to prevent hanging
try:
    response = requests.get("https://api.example.com/data", timeout=10)
except requests.exceptions.Timeout:
    print("Request took too long!")
```

---

## 26.6 Working with JSON Response Data

### Navigating Nested JSON

```python
import requests

response = requests.get("https://api.github.com/users/octocat")
user = response.json()

# Access nested data
print(user["login"])          # octocat
print(user["name"])           # The Octocat
print(user["public_repos"])   # 8

# Handle missing keys safely
bio = user.get("bio", "No bio available")
print(bio)
```

### Processing Lists from API

```python
response = requests.get("https://jsonplaceholder.typicode.com/users")
users = response.json()  # List of user dicts

print(f"{'Name':<25} {'Email':<30} {'City'}")
print("-" * 70)
for user in users:
    name = user["name"]
    email = user["email"]
    city = user["address"]["city"]
    print(f"{name:<25} {email:<30} {city}")
```

### Saving API Data to File

```python
import requests
import json
import csv

# Fetch data
response = requests.get("https://jsonplaceholder.typicode.com/posts")
posts = response.json()

# Save as JSON
with open("posts.json", "w") as f:
    json.dump(posts, f, indent=4)

# Save as CSV
with open("posts.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.DictWriter(f, fieldnames=["id", "userId", "title", "body"])
    writer.writeheader()
    writer.writerows(posts)

print(f"Saved {len(posts)} posts to JSON and CSV.")
```

---

## 26.7 API Authentication

### API Key in Headers

```python
headers = {
    "X-API-Key": "your-api-key-here"
}
response = requests.get("https://api.example.com/data", headers=headers)
```

### Bearer Token

```python
headers = {
    "Authorization": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
response = requests.get("https://api.example.com/protected", headers=headers)
```

### API Key in Query Parameters

```python
params = {
    "api_key": "your-api-key-here",
    "city": "Delhi"
}
response = requests.get("https://api.example.com/weather", params=params)
```

### Storing API Keys Securely

```python
import os
from dotenv import load_dotenv

load_dotenv()  # Load from .env file
api_key = os.getenv("API_KEY")

if not api_key:
    raise ValueError("API_KEY not found in environment variables")

headers = {"Authorization": f"Bearer {api_key}"}
```

```
# .env file (add to .gitignore!)
API_KEY=your-secret-key-here
```

> **Never hardcode API keys in source code.** Use environment variables or `.env` files.

---

## 26.8 Rate Limiting and Pagination

### Handling Rate Limits

```python
import time

def fetch_with_retry(url, max_retries=3, delay=2):
    """Fetch URL with retry on rate limit."""
    for attempt in range(max_retries):
        response = requests.get(url)
        
        if response.ok:
            return response.json()
        elif response.status_code == 429:
            wait = int(response.headers.get("Retry-After", delay))
            print(f"Rate limited. Waiting {wait}s... (attempt {attempt+1})")
            time.sleep(wait)
        else:
            response.raise_for_status()
    
    raise Exception(f"Failed after {max_retries} retries")
```

### Pagination

```python
def fetch_all_pages(base_url, per_page=100):
    """Fetch all pages from a paginated API."""
    all_items = []
    page = 1
    
    while True:
        params = {"page": page, "per_page": per_page}
        response = requests.get(base_url, params=params)
        response.raise_for_status()
        
        data = response.json()
        if not data:
            break
        
        all_items.extend(data)
        print(f"Page {page}: {len(data)} items")
        page += 1
    
    return all_items

# Usage
repos = fetch_all_pages("https://api.github.com/users/octocat/repos")
print(f"Total repos: {len(repos)}")
```

---

## 26.9 Popular Free APIs for Practice

| API | URL | Auth | Data |
|-----|-----|------|------|
| JSONPlaceholder | jsonplaceholder.typicode.com | None | Fake posts, users, comments |
| GitHub | api.github.com | Optional | Repos, users, commits |
| Open-Meteo | open-meteo.com/en/docs | None | Weather forecasts |
| REST Countries | restcountries.com | None | Country information |
| CoinGecko | api.coingecko.com | None | Cryptocurrency data |
| Dog CEO | dog.ceo/dog-api | None | Random dog images |
| JokeAPI | v2.jokeapi.dev | None | Programming jokes |

---

## 🔧 Hands-On Activity: API Data Fetcher

**Duration:** 25 minutes

Create a file `session26_api.py`:

```python
# Session 26 — Working with APIs
import requests
import json

# Part 1: Fetch GitHub User
print("=== Part 1: GitHub User ===")
username = "octocat"
response = requests.get(f"https://api.github.com/users/{username}", timeout=10)

if response.ok:
    user = response.json()
    print(f"  User: {user['login']}")
    print(f"  Name: {user.get('name', 'N/A')}")
    print(f"  Public Repos: {user['public_repos']}")
    print(f"  Followers: {user['followers']}")
    print(f"  Created: {user['created_at'][:10]}")
else:
    print(f"  Error: {response.status_code}")

# Part 2: Fetch Posts and Save
print("\n=== Part 2: Fetch & Save Posts ===")
response = requests.get("https://jsonplaceholder.typicode.com/posts", timeout=10)

if response.ok:
    posts = response.json()
    print(f"  Fetched {len(posts)} posts")
    
    # Display first 5
    for post in posts[:5]:
        print(f"  [{post['id']}] {post['title'][:50]}...")
    
    # Save to JSON
    with open("api_posts.json", "w") as f:
        json.dump(posts[:10], f, indent=4)
    print("  Saved 10 posts to api_posts.json")

# Part 3: Fetch Country Data
print("\n=== Part 3: Country Info ===")
try:
    response = requests.get("https://restcountries.com/v3.1/name/india", timeout=10)
    if response.ok:
        country = response.json()[0]
        print(f"  Name: {country['name']['common']}")
        print(f"  Capital: {country['capital'][0]}")
        print(f"  Population: {country['population']:,}")
        print(f"  Region: {country['region']}")
        print(f"  Languages: {', '.join(country['languages'].values())}")
    else:
        print(f"  Error: {response.status_code}")
except requests.exceptions.RequestException as e:
    print(f"  Request failed: {e}")

# Part 4: Error Handling Demo
print("\n=== Part 4: Error Handling ===")
test_urls = [
    ("Valid", "https://api.github.com"),
    ("Not Found", "https://api.github.com/nonexistent-endpoint-xyz"),
    ("Bad Domain", "https://this-domain-does-not-exist-xyz.com"),
]

for label, url in test_urls:
    try:
        r = requests.get(url, timeout=5)
        print(f"  {label}: Status {r.status_code} {'✅' if r.ok else '❌'}")
    except requests.exceptions.ConnectionError:
        print(f"  {label}: Connection failed ❌")
    except requests.exceptions.Timeout:
        print(f"  {label}: Timed out ❌")

print("\nDone!")
```

---

## Session 26 — Key Takeaways

1. **APIs** enable programs to communicate — your Python code can fetch data from the web
2. **`requests.get(url)`** makes HTTP GET requests; `.json()` parses the JSON response
3. **Always check `response.status_code`** or use `response.raise_for_status()`
4. **Handle errors:** ConnectionError, Timeout, HTTPError — APIs are unreliable by nature
5. **Never hardcode API keys** — use environment variables or `.env` files
6. **Save API data** to JSON/CSV for offline processing

---

## Preparation for Session 27
- Practice: Fetch weather data for your city using Open-Meteo API
- Think about: What repetitive tasks could you automate with Python?
- Review: What is file system automation? What is web scraping?

---

*Session 26 of 30 | Module 6: Automation & Capstone Project*
*Professional Python Programming Certification — UpSkill Global Education Technologies Inc., Canada*
