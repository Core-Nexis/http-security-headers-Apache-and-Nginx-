# Security Headers Configuration for Nginx and Apache

This repository provides a comprehensive guide and ready-to-use configurations for implementing essential security headers in web servers like **Nginx** and **Apache**. These headers enhance the security of your web application by mitigating various vulnerabilities.

## Overview
Security headers are HTTP response headers that help protect your website from common security threats like clickjacking, cross-site scripting (XSS), and MIME type sniffing. This repository includes:

- Predefined security headers for both **Nginx** and **Apache**.
- Detailed explanations of each header's purpose.
- A tool to verify the implementation of security headers.

---

## Security Headers Implemented

| Header Name            | Purpose                                                                                 |
|------------------------|-----------------------------------------------------------------------------------------|
| **X-Content-Type-Options** | Prevents browsers from MIME-sniffing the response away from the declared Content-Type.    |
| **X-Frame-Options**       | Protects against clickjacking by controlling whether your website can be embedded in iframes. |
| **X-XSS-Protection**      | Enables browser's built-in XSS protection and prevents rendering of malicious scripts.     |
| **Referrer-Policy**       | Controls how much referrer information is included with requests.                          |
| **Permissions-Policy**    | Manages access to browser features like geolocation, camera, and microphone.                |

---

## Configuration Files

### Nginx Configuration
To use these security headers in an Nginx server, add the following code to your configuration file (`nginx.conf` or site-specific file in `sites-available`):

```nginx
add_header X-Content-Type-Options "nosniff";
add_header X-Frame-Options "SAMEORIGIN";
add_header X-XSS-Protection "1; mode=block";
add_header Referrer-Policy "strict-origin";
add_header Permissions-Policy "fullscreen=(self), clipboard-write=(self), geolocation=(), camera=(), microphone=()";
```

### Apache Configuration
To use these security headers in an Apache server, add the following code to your `.htaccess` file or the main configuration file:

```apache
<IfModule mod_headers.c>
    Header set X-Content-Type-Options "nosniff"
    Header set X-Frame-Options "SAMEORIGIN"
    Header set X-XSS-Protection "1; mode=block"
    Header set Referrer-Policy "strict-origin"
    Header set Permissions-Policy "fullscreen=(self), clipboard-write=(self), geolocation=(), camera=(), microphone=()"
</IfModule>
```

---

## Verify Your Security Headers
After implementing the headers, you can verify their presence and correctness using the following online tool:

🔗 [Security Headers Test Tool](https://tools.corenexis.com/web/security-headers)

Enter your website URL to see which headers are active and identify any potential issues.

---

## How These Headers Work

### 1. **X-Content-Type-Options**
- **Value**: `nosniff`
- Ensures that browsers respect the declared `Content-Type` and do not attempt to guess the MIME type.

### 2. **X-Frame-Options**
- **Value**: `SAMEORIGIN`
- Restricts embedding of your site in iframes to only the same origin, preventing clickjacking attacks.

### 3. **X-XSS-Protection**
- **Value**: `1; mode=block`
- Activates the browser's XSS filter to block potentially malicious scripts instead of rendering them.

### 4. **Referrer-Policy**
- **Value**: `strict-origin`
- Limits the amount of referrer information shared with external sites, improving user privacy.

### 5. **Permissions-Policy**
- **Value**: `fullscreen=(self), clipboard-write=(self), geolocation=(), camera=(), microphone=()`
- Specifies which features can be accessed by your site or embedded resources.

---

## Getting Started
### Steps to Use
1. Copy the relevant configuration block for your web server (Nginx or Apache).
2. Paste the code into your server's configuration file or `.htaccess` file.
3. Restart your server to apply the changes:
   - For Nginx: `sudo systemctl reload nginx`
   - For Apache: `sudo systemctl restart apache2`

4. Test your implementation using the [Security Headers Test Tool](https://tools.corenexis.com/web/security-headers).

---

## Contributing
If you find any issues or want to suggest additional security headers, feel free to open an issue or submit a pull request.

---

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
