# 🌍 BooLe Mobile App API Documentation

Comprehensive REST API documentation for **BooLe Apps** - Your companion for exploring Indonesian destinations, cultural heritage, and emergency services.

[![Supabase](https://img.shields.io/badge/Database-Supabase-3ECF8E?logo=supabase)](https://supabase.com)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?logo=postgresql)](https://www.postgresql.org)
[![API Status](https://img.shields.io/badge/Status-Active-success)]()

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Getting Started](#-getting-started)
- [Authentication](#-authentication)
- [API Endpoints](#-api-endpoints)
  - [Destinations](#-destinations)
  - [Culture & Education](#-culture--education)
  - [Emergency Services](#-emergency-services)
- [Error Handling](#-error-handling)
- [Rate Limiting](#-rate-limiting)
- [Code Examples](#-code-examples)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

BooLe API provides a robust backend infrastructure built on **Supabase Postgres** to deliver:

- **🏖️ Tourism Destinations** - Comprehensive data on tourist attractions across Indonesia
- **🎭 Cultural Education** - Rich information about local customs, languages, and traditions
- **🚨 Emergency Services** - Quick access to critical emergency contacts nationwide
- **⚡ Real-time Updates** - Live data synchronization
- **🔒 Secure Access** - Protected endpoints with API key authentication
- **📱 Mobile-First** - Optimized for mobile app integration

### Key Features

- RESTful API architecture
- JSON response format
- Row Level Security (RLS) enabled
- Automatic timestamps
- Multi-language support
- Geolocation data

---

## 🚀 Getting Started

### Base URL

```
https://fowfuytbmgxpeogsaiwk.supabase.co
```

### Prerequisites

- Valid Supabase API key
- HTTP client (curl, Postman, or programming language HTTP library)
- Basic understanding of REST APIs

### Quick Start

1. **Obtain API Credentials**
   - Get your `SUPABASE_URL` and `SUPABASE_ANON_KEY` from Supabase dashboard
   - Store credentials securely (use environment variables)

2. **Make Your First Request**
   ```bash
   curl -X GET \
     'https://fowfuytbmgxpeogsaiwk.supabase.co/rest/v1/destinations' \
     -H 'apikey: YOUR_API_KEY' \
     -H 'Authorization: Bearer YOUR_API_KEY'
   ```

3. **Process Response**
   - All responses are in JSON format
   - Check HTTP status codes for success/errors

---

## 🔐 Authentication

All API requests require authentication using API keys in request headers.

### Required Headers

| Header | Value | Description |
|--------|-------|-------------|
| `apikey` | `YOUR_API_KEY` | Supabase anonymous or service key |
| `Authorization` | `Bearer YOUR_API_KEY` | Bearer token for authentication |
| `Content-Type` | `application/json` | Required for POST/PUT/PATCH requests |

### Environment Setup

**Using .env file:**
```bash
SUPABASE_URL=https://fowfuytbmgxpeogsaiwk.supabase.co
SUPABASE_ANON_KEY=your_anon_key_here
```

**Using Flutter/Dart (ENVIED):**
```dart
import 'package:envied/envied.dart';

part 'env.g.dart';

@Envied(path: '.env')
abstract class Env {
  @EnviedField(varName: 'SUPABASE_URL', obfuscate: true)
  static final String supabaseUrl = _Env.supabaseUrl;
  
  @EnviedField(varName: 'SUPABASE_ANON_KEY', obfuscate: true)
  static final String supabaseAnonKey = _Env.supabaseAnonKey;
}
```

---

## 🛣️ API Endpoints

### 🏖️ Destinations

Manage and retrieve tourist destination data across Indonesia.

#### Get All Destinations

```http
GET /rest/v1/destinations
```

**Query Parameters:**

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| `province` | string | Filter by province name | `province=eq.Bali` |
| `city` | string | Filter by city name | `city=eq.Batam` |
| `category` | string | Filter by destination type | `category=eq.Beach` |
| `rating` | number | Filter by minimum rating | `rating=gte.4.5` |
| `limit` | integer | Limit results (default: 10) | `limit=20` |
| `offset` | integer | Pagination offset | `offset=10` |
| `order` | string | Sort results | `order=rating.desc` |

**Supabase Query Operators:**
- `eq` - equals
- `neq` - not equals
- `gt` - greater than
- `gte` - greater than or equal
- `lt` - less than
- `lte` - less than or equal
- `like` - pattern matching
- `ilike` - case-insensitive pattern matching

**Example Request:**
```bash
curl -X GET \
  'https://fowfuytbmgxpeogsaiwk.supabase.co/rest/v1/destinations?province=eq.Bali&limit=10&order=rating.desc' \
  -H 'apikey: YOUR_API_KEY' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

**Response (200 OK):**
```json
[
  {
    "id": "97eb9785-9612-4d73-bf55-d4d1f2330d93",
    "name": "Nongsa Beach",
    "description": "A beach with white sand and a scenic view of Singapore from afar.",
    "city": "Batam",
    "province": "Riau Islands",
    "latitude": 1.234567,
    "longitude": 104.123456,
    "category": "Beach",
    "rating": 4.6,
    "ticket_price": 20000,
    "facilities": [
      "Toilet",
      "Food Stalls",
      "Parking Area",
      "Accommodation"
    ],
    "opening_hours": {
      "monday": "08:00-18:00",
      "tuesday": "08:00-18:00",
      "wednesday": "08:00-18:00",
      "thursday": "08:00-18:00",
      "friday": "08:00-18:00",
      "saturday": "07:00-19:00",
      "sunday": "07:00-19:00"
    },
    "image_urls": [
      "https://i.postimg.cc/8zfRfkgd/IMG-20210930-WA0091.jpg",
      "https://i.postimg.cc/25z5RTGm/pantai-nongsa-batam-riau.jpg",
      "https://i.postimg.cc/2y46Ntsm/3454b-montego-resort-di-nongsa-batam.jpg"
    ],
    "created_at": "2025-10-10T08:01:00.989309+00:00",
    "updated_at": "2025-10-10T08:01:00.989309+00:00"
  }
]
```

#### Get Single Destination

```http
GET /rest/v1/destinations?id=eq.{destination_id}
```

**Response:** Single destination object in array format

---

### 🎭 Culture & Education

Access cultural information, traditions, and educational content about Indonesian provinces.

#### Get All Cultures

```http
GET /rest/v1/culture
```

**Query Parameters:**

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| `province` | string | Filter by province name | `province=eq.Bali` |
| `region` | string | Filter by geographical region | `region=eq.Sulawesi` |
| `province_code` | string | Filter by province code | `province_code=eq.BA` |
| `limit` | integer | Limit results | `limit=5` |
| `order` | string | Sort results | `order=province.asc` |

**Example Request:**
```bash
curl -X GET \
  'https://fowfuytbmgxpeogsaiwk.supabase.co/rest/v1/culture?region=eq.Java' \
  -H 'apikey: YOUR_API_KEY' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

**Response (200 OK):**
```json
[
  {
    "id": "41a574f4-8c9a-4e02-b28a-f0ab12ca8839",
    "province": "South Sulawesi",
    "province_code": "SS",
    "region": "Sulawesi",
    "local_languages": ["Bugis", "Makassarese"],
    "primary_language": "Bugis",
    "greeting_phrases": {
      "common": [
        {
          "phrase": "Assalamu'alaikum",
          "translation": "Peace be upon you"
        }
      ],
      "formal": [
        {
          "phrase": "Selamat pagi",
          "translation": "Good morning"
        }
      ]
    },
    "dress_code": {
      "men": "Sarong and traditional shirts",
      "women": "Kebaya and sarong"
    },
    "social_etiquette": {
      "family": "Strong kinship ties",
      "greetings": "Handshake and slight nod"
    },
    "taboos": {
      "mourning": "Respectful behavior at funerals"
    },
    "religious_practices": {
      "practices": "Mosque attendance and festivals",
      "predominant_religion": "Islam"
    },
    "cultural_highlights": {
      "heritage": "Maritime traditions",
      "landmarks": ["Fort Rotterdam", "Bontosunggu"]
    },
    "traditional_arts": {
      "dance": ["Pakarena"],
      "crafts": ["Pottery"]
    },
    "culinary_customs": {
      "dishes": ["Coto Makassar", "Konro"],
      "flavors": "Rich broth-based dishes"
    },
    "festivals": {
      "major": ["Maulid Nabi"]
    },
    "description": "South Sulawesi is noted for its seafaring history and robust cuisine.",
    "visitor_tips": [
      "Respect local fishing communities",
      "Ask before photographing ceremonies"
    ],
    "image_urls": [
      "https://i.imgur.com/HaUVS1N.jpeg",
      "https://i.imgur.com/jxklGM6.jpeg",
      "https://i.imgur.com/7ozdRFW.jpeg"
    ],
    "created_at": "2025-10-11T10:04:11.548343+00:00"
  }
]
```

---

### 🚨 Emergency Services

Access emergency contact information for hospitals, police, fire departments, and other critical services.

#### Get All Emergency Services

```http
GET /rest/v1/emergency_services
```

**Query Parameters:**

| Parameter | Type | Description | Example |
|-----------|------|-------------|---------|
| `category` | string | Filter by service type | `category=eq.hospital` |
| `coverage_level` | string | Filter by coverage (national/provincial/city) | `coverage_level=eq.national` |
| `coverage_code` | string | Filter by area code | `coverage_code=eq.ID` |
| `priority` | integer | Filter by priority level | `priority=lte.3` |
| `order` | string | Sort results | `order=priority.asc` |

**Available Categories:**
- `police` - Law enforcement
- `fire` - Fire department
- `ambulance` - Medical emergency
- `hospital` - Healthcare facilities
- `search_rescue` - SAR teams
- `disaster` - Disaster management

**Example Request:**
```bash
curl -X GET \
  'https://fowfuytbmgxpeogsaiwk.supabase.co/rest/v1/emergency_services?category=eq.hospital&coverage_level=eq.city' \
  -H 'apikey: YOUR_API_KEY' \
  -H 'Authorization: Bearer YOUR_API_KEY'
```

**Response (200 OK):**
```json
[
  {
    "id": "302d00bd-0d7d-492c-8abb-0050bb7bae52",
    "name": "Police",
    "category": "police",
    "description": "National police emergency service for crime reports, accidents, and other emergency situations",
    "coverage_level": "national",
    "coverage_code": "ID",
    "coverage_name": "Indonesia",
    "latitude": null,
    "longitude": null,
    "languages": ["id", "en"],
    "contact_hours": "24/7",
    "priority": 1,
    "verified_at": "2025-10-21T04:24:28.743109+00:00",
    "source_name": "Indonesian National Police (POLRI)",
    "source_url": "https://www.polri.go.id",
    "source_type": "official",
    "tags": ["emergency", "crime", "accident", "security"],
    "metadata": {},
    "created_at": "2025-10-21T04:24:28.743109+00:00",
    "updated_at": "2025-10-21T04:24:28.743109+00:00"
  }
]
```

---

## ⚠️ Error Handling

The API uses standard HTTP status codes and returns detailed error messages.

### HTTP Status Codes

| Code | Status | Description |
|------|--------|-------------|
| 200 | OK | Request successful |
| 201 | Created | Resource created successfully |
| 400 | Bad Request | Invalid request parameters |
| 401 | Unauthorized | Missing or invalid API key |
| 403 | Forbidden | Insufficient permissions |
| 404 | Not Found | Resource not found |
| 406 | Not Acceptable | Invalid Accept header |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Server error |
| 503 | Service Unavailable | Service temporarily unavailable |

### Error Response Format

```json
{
  "code": "PGRST116",
  "message": "The result contains 0 rows",
  "details": null,
  "hint": null
}
```

### Common Error Examples

**401 Unauthorized:**
```json
{
  "message": "Invalid API key"
}
```

**400 Bad Request:**
```json
{
  "code": "PGRST102",
  "message": "column destinations.invalid_field does not exist",
  "details": null,
  "hint": null
}
```

---

## 📊 Rate Limiting

To ensure fair usage and service stability:

- **Default Rate Limit:** 100 requests per minute per API key
- **Burst Limit:** 20 requests per second
- Rate limit headers included in responses:
  - `X-RateLimit-Limit`: Maximum requests allowed
  - `X-RateLimit-Remaining`: Requests remaining
  - `X-RateLimit-Reset`: Time when limit resets (Unix timestamp)

**Best Practices:**
- Implement exponential backoff for retries
- Cache responses when appropriate
- Use pagination for large datasets
- Monitor rate limit headers

---

## 💻 Code Examples

### Flutter/Dart Implementation

**Client Setup:**
```dart
import 'package:http/http.dart' as http;
import 'dart:convert';

class BooLeApiClient {
  final String baseUrl;
  final String apiKey;
  final http.Client client;

  BooLeApiClient({
    required this.baseUrl,
    required this.apiKey,
    http.Client? client,
  }) : client = client ?? http.Client();

  Map<String, String> get _headers => {
    'apikey': apiKey,
    'Authorization': 'Bearer $apiKey',
    'Content-Type': 'application/json',
  };

  Future<List<dynamic>> getDestinations({
    String? province,
    String? category,
    int? limit,
  }) async {
    final queryParams = <String, String>{};
    if (province != null) queryParams['province'] = 'eq.$province';
    if (category != null) queryParams['category'] = 'eq.$category';
    if (limit != null) queryParams['limit'] = limit.toString();

    final uri = Uri.parse('$baseUrl/rest/v1/destinations')
        .replace(queryParameters: queryParams);

    final response = await client.get(uri, headers: _headers);

    if (response.statusCode == 200) {
      return json.decode(response.body) as List<dynamic>;
    } else {
      throw Exception('Failed to load destinations: ${response.body}');
    }
  }

  Future<List<dynamic>> getCulture({String? region}) async {
    final queryParams = <String, String>{};
    if (region != null) queryParams['region'] = 'eq.$region';

    final uri = Uri.parse('$baseUrl/rest/v1/culture')
        .replace(queryParameters: queryParams);

    final response = await client.get(uri, headers: _headers);

    if (response.statusCode == 200) {
      return json.decode(response.body) as List<dynamic>;
    } else {
      throw Exception('Failed to load culture data: ${response.body}');
    }
  }

  Future<List<dynamic>> getEmergencyServices({
    String? category,
    String? coverageLevel,
  }) async {
    final queryParams = <String, String>{
      'order': 'priority.asc',
    };
    if (category != null) queryParams['category'] = 'eq.$category';
    if (coverageLevel != null) {
      queryParams['coverage_level'] = 'eq.$coverageLevel';
    }

    final uri = Uri.parse('$baseUrl/rest/v1/emergency_services')
        .replace(queryParameters: queryParams);

    final response = await client.get(uri, headers: _headers);

    if (response.statusCode == 200) {
      return json.decode(response.body) as List<dynamic>;
    } else {
      throw Exception('Failed to load emergency services: ${response.body}');
    }
  }

  void dispose() {
    client.close();
  }
}
```

**Usage Example:**
```dart
void main() async {
  final client = BooLeApiClient(
    baseUrl: Env.supabaseUrl,
    apiKey: Env.supabaseAnonKey,
  );

  try {
    // Get destinations in Bali
    final destinations = await client.getDestinations(
      province: 'Bali',
      limit: 10,
    );
    print('Found ${destinations.length} destinations');

    // Get culture info for Java region
    final cultures = await client.getCulture(region: 'Java');
    print('Found ${cultures.length} culture entries');

    // Get emergency services
    final emergencyServices = await client.getEmergencyServices(
      category: 'hospital',
      coverageLevel: 'national',
    );
    print('Found ${emergencyServices.length} emergency services');
  } catch (e) {
    print('Error: $e');
  } finally {
    client.dispose();
  }
}
```

### JavaScript/TypeScript Example

```typescript
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = process.env.SUPABASE_URL!;
const supabaseKey = process.env.SUPABASE_ANON_KEY!;
const supabase = createClient(supabaseUrl, supabaseKey);

// Get destinations
async function getDestinations(filters?: {
  province?: string;
  category?: string;
  limit?: number;
}) {
  let query = supabase.from('destinations').select('*');
  
  if (filters?.province) {
    query = query.eq('province', filters.province);
  }
  if (filters?.category) {
    query = query.eq('category', filters.category);
  }
  if (filters?.limit) {
    query = query.limit(filters.limit);
  }

  const { data, error } = await query;
  
  if (error) throw error;
  return data;
}

// Get culture data
async function getCultureData(region?: string) {
  let query = supabase.from('culture').select('*');
  
  if (region) {
    query = query.eq('region', region);
  }

  const { data, error } = await query;
  
  if (error) throw error;
  return data;
}

// Get emergency services
async function getEmergencyServices(filters?: {
  category?: string;
  coverageLevel?: string;
}) {
  let query = supabase
    .from('emergency_services')
    .select('*')
    .order('priority', { ascending: true });
  
  if (filters?.category) {
    query = query.eq('category', filters.category);
  }
  if (filters?.coverageLevel) {
    query = query.eq('coverage_level', filters.coverageLevel);
  }

  const { data, error } = await query;
  
  if (error) throw error;
  return data;
}
```

### Python Example

```python
import os
import requests
from typing import Optional, List, Dict

class BooLeAPI:
    def __init__(self, base_url: str, api_key: str):
        self.base_url = base_url
        self.headers = {
            'apikey': api_key,
            'Authorization': f'Bearer {api_key}',
            'Content-Type': 'application/json'
        }
    
    def get_destinations(
        self,
        province: Optional[str] = None,
        category: Optional[str] = None,
        limit: Optional[int] = None
    ) -> List[Dict]:
        params = {}
        if province:
            params['province'] = f'eq.{province}'
        if category:
            params['category'] = f'eq.{category}'
        if limit:
            params['limit'] = str(limit)
        
        response = requests.get(
            f'{self.base_url}/rest/v1/destinations',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()
    
    def get_culture(self, region: Optional[str] = None) -> List[Dict]:
        params = {}
        if region:
            params['region'] = f'eq.{region}'
        
        response = requests.get(
            f'{self.base_url}/rest/v1/culture',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()
    
    def get_emergency_services(
        self,
        category: Optional[str] = None,
        coverage_level: Optional[str] = None
    ) -> List[Dict]:
        params = {'order': 'priority.asc'}
        if category:
            params['category'] = f'eq.{category}'
        if coverage_level:
            params['coverage_level'] = f'eq.{coverage_level}'
        
        response = requests.get(
            f'{self.base_url}/rest/v1/emergency_services',
            headers=self.headers,
            params=params
        )
        response.raise_for_status()
        return response.json()

# Usage
api = BooLeAPI(
    base_url=os.getenv('SUPABASE_URL'),
    api_key=os.getenv('SUPABASE_ANON_KEY')
)

destinations = api.get_destinations(province='Bali', limit=10)
print(f'Found {len(destinations)} destinations')
```

---

## 🧪 Testing

### Using Postman

1. **Create New Request**
   - Method: GET
   - URL: `https://fowfuytbmgxpeogsaiwk.supabase.co/rest/v1/destinations`

2. **Add Headers**
   - Key: `apikey`, Value: `YOUR_API_KEY`
   - Key: `Authorization`, Value: `Bearer YOUR_API_KEY`

3. **Add Query Parameters** (Optional)
   - `province`: `eq.Bali`
   - `limit`: `10`

4. **Send Request** and inspect response

### Using cURL

**Test Destinations Endpoint:**
```bash
curl -X GET \
  'https://fowfuytbmgxpeogsaiwk.supabase.co/rest/v1/destinations?limit=5' \
  -H 'apikey: YOUR_API_KEY' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  | jq '.'
```

**Test with Filters:**
```bash
curl -X GET \
  'https://fowfuytbmgxpeogsaiwk.supabase.co/rest/v1/destinations?province=eq.Bali&category=eq.Beach' \
  -H 'apikey: YOUR_API_KEY' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  | jq '.'
```

---

## 📚 Additional Resources

### Supabase Documentation
- [Supabase REST API Guide](https://supabase.com/docs/guides/api)
- [PostgREST Documentation](https://postgrest.org/en/stable/)
- [Supabase Client Libraries](https://supabase.com/docs/reference)

### Community & Support
- [GitHub Issues](../../issues) - Report bugs or request features
- [Supabase Discord](https://discord.supabase.com) - Community support
- [Stack Overflow](https://stackoverflow.com/questions/tagged/supabase) - Q&A

---

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Development Setup

1. **Fork the Repository**
   ```bash
   git clone https://github.com/yourusername/boole-mobile-app-api.git
   cd boole-mobile-app-api
   ```

2. **Create Feature Branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```

3. **Make Changes**
   - Write clear, descriptive commit messages
   - Follow existing code style
   - Add tests if applicable
   - Update documentation

4. **Commit Changes**
   ```bash
   git commit -m "feat: add amazing feature"
   ```

5. **Push to Branch**
   ```bash
   git push origin feature/amazing-feature
   ```

6. **Open Pull Request**
   - Describe your changes clearly
   - Reference any related issues
   - Wait for review

### Contribution Guidelines

- Follow [Conventional Commits](https://www.conventionalcommits.org/)
- Write meaningful commit messages
- Keep PRs focused and atomic
- Add documentation for new features
- Ensure backward compatibility

### Code of Conduct

- Be respectful and inclusive
- Provide constructive feedback
- Help others learn and grow
- Follow community guidelines

---

## 🔄 Changelog

### Version 1.0.0 (2025-10-26)
- Initial API release
- Destinations endpoint
- Culture endpoint
- Emergency services endpoint
- Complete documentation

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### MIT License Summary

```
Copyright (c) 2025 Sande Okta Effendi

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

## 🙏 Acknowledgments

- **Supabase Team** - For the amazing platform
- **Dicoding Indonesia** - For amazing learning journey
- **Boole Mobile App's Team** - For making this project better

---

## 📞 Support

Need help? Have questions?

- 📖 Check the [Documentation](#-table-of-contents)
- 🐛 [Report Bugs](../../issues/new?template=bug_report.md)
- 💡 [Request Features](../../issues/new?template=feature_request.md)
- 💬 [Join Discussions](../../discussions)

---

<div align="center">

**Made with ❤️ for Indonesian Tourism**

⭐ Star this repo if you find it helpful!

[Report Bug](../../issues) · [Request Feature](../../issues) · [Documentation](#)

</div>