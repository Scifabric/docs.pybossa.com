### Help API

**Endpoint: /help/api**

*Allowed methods*: **GET**

**GET**

Gives you the API help for your PYBOSSA

-   **project\_id**: a project id for the help example text. If no
    project exists it is null.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "project_id": 1104,
  "template": "help/privacy.html",
  "title": "API Help"
}
```

### Help privacy

**Endpoint: /help/privacy**

*Allowed methods*: **GET**

**GET**

Gives you the privacy policy for your PYBOSSA

-   **content**: Simplified HTML of rendered privacy policy.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "content": "<html><body><p>privacy policy here</p></body></html>"
  "template": "help/privacy.html",
  "title": "Privacy Policy"
}
```

### Help cookie policy

**Endpoint: /help/cookies-policy**

*Allowed methods*: **GET**

**GET**

Gives you the cookie policy for your PYBOSSA

-   **content**: Simplified HTML of rendered cookie policy.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "content": "<html><body><p>cookie policy here</p></body></html>"
  "template": "help/cookies_policy.html",
  "title": "Help: Cookies Policy"
}
```

### Help terms of use

**Endpoint: /help/terms-of-use**

*Allowed methods*: **GET**

**GET**

Gives you the terms of use for your PYBOSSA

-   **content**: Simplified HTML of rendered terms of use.
-   **template**: The Jinja2 template that could be rendered.
-   **title**: the title for the endpoint.

**Example output**

```json
{
  "content": "<html><body><p>Terms of use text</p></body></html>"
  "template": "help/tos.html",
  "title": "Help: Terms of Use"
}
```


