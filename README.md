# Python Substack

A Python wrapper around the Substack API for creating, managing, and publishing posts programmatically.

## Features

- 🚀 Create and publish posts to Substack
- 📝 Support for draft posts
- 📊 Get subscriber count and analytics
- 🖼️ Image upload support
- ⏰ Post scheduling functionality
- 🔐 Authentication handling
- 🛡️ Rate limiting protection

## Installation

### Using Poetry (Recommended)

```bash
# Clone the repository
git clone https://github.com/TarunVedula/python-substack.git
cd python-substack

# Install dependencies
poetry install

# Activate the virtual environment
poetry shell
```

### Using pip

```bash
pip install python-substack
```

## Quick Start

### 1. Set up Authentication

Create a `.env` file in your project directory:

```env
SUBSTACK_EMAIL=your-email@example.com
SUBSTACK_PASSWORD=your-password
```

### 2. Basic Usage

```python
from substack import SubstackAPI
import os
from dotenv import load_dotenv

# Load environment variables
load_dotenv()

# Initialize the API client
api = SubstackAPI(
    email=os.getenv("SUBSTACK_EMAIL"),
    password=os.getenv("SUBSTACK_PASSWORD")
)

# Get subscriber count
subscriber_count = api.get_subscriber_count()
print(f"Current subscribers: {subscriber_count}")

# Create a new post
post_data = {
    "title": "My First API Post",
    "subtitle": "Created using python-substack",
    "body": "This post was created programmatically using the python-substack library!",
    "published": True
}

post = api.create_post(post_data)
print(f"Post created: {post.title}")
```

## Examples

### Publishing a Post

```python
from substack import SubstackAPI

api = SubstackAPI(email="your-email@example.com", password="your-password")

post_data = {
    "title": "Hello World",
    "subtitle": "A test post",
    "body": "# Hello World\n\nThis is a test post created with python-substack.",
    "published": True
}

post = api.create_post(post_data)
print(f"Published: {post.url}")
```

### Creating a Draft

```python
post_data = {
    "title": "Draft Post",
    "subtitle": "This is a draft",
    "body": "This post is saved as a draft.",
    "published": False
}

draft = api.create_post(post_data)
print(f"Draft created: {draft.id}")
```

### Getting Subscriber Count

```python
subscriber_count = api.get_subscriber_count()
print(f"You have {subscriber_count} subscribers")
```

### Uploading Images

```python
# Upload an image
image_url = api.upload_image("path/to/image.jpg")

# Use the image in a post
post_data = {
    "title": "Post with Image",
    "body": f"Here's an image: ![Image]({image_url})",
    "published": True
}

post = api.create_post(post_data)
```

## API Reference

### SubstackAPI Class

#### Methods

- `create_post(post_data)`: Create a new post
- `get_subscriber_count()`: Get current subscriber count
- `upload_image(image_path)`: Upload an image
- `schedule_post(post_data, publish_date)`: Schedule a post for later publication

#### Post Data Structure

```python
post_data = {
    "title": str,           # Required: Post title
    "subtitle": str,        # Optional: Post subtitle
    "body": str,           # Required: Post content (supports Markdown)
    "published": bool,     # Required: Whether to publish immediately
    "tags": list,          # Optional: List of tags
    "section": str         # Optional: Section name
}
```

## Configuration

### Environment Variables

- `SUBSTACK_EMAIL`: Your Substack email address
- `SUBSTACK_PASSWORD`: Your Substack password

### Rate Limiting

The library automatically handles Substack's rate limiting. If you encounter rate limit errors, the library will wait and retry automatically.

## Development

### Setting up Development Environment

```bash
# Clone the repository
git clone https://github.com/TarunVedula/python-substack.git
cd python-substack

# Install dependencies
poetry install

# Install pre-commit hooks
pre-commit install

# Run tests
poetry run pytest
```

### Running Tests

```bash
poetry run pytest
```

### Code Quality

This project uses:
- **Poetry** for dependency management
- **pytest** for testing
- **pre-commit** for code quality hooks
- **GitHub Actions** for CI/CD

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Original project by Paolo Mazza
- Substack API for providing the underlying service

## Support

If you encounter any issues or have questions, please:

1. Check the [examples](examples/) directory for usage examples
2. Open an issue on GitHub
3. Review the existing issues for similar problems

---

**Note**: This library is not officially affiliated with Substack. Use at your own risk and in accordance with Substack's terms of service. 