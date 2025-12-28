# Contributing to Transformer From Scratch

Thank you for your interest in contributing to this project! This document provides guidelines and instructions for contributing.

## Development Setup

### 1. Clone the Repository

```bash
git clone https://github.com/charansoma3001/transformerkit.git
cd transformerkit
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Development Dependencies

```bash
pip install -e ".[dev]"
# Or using requirements files:
pip install -r requirements-dev.txt
```

## Code Style

This project follows Python best practices and uses automated tools for code quality.

### Code Formatting

We use [Black](https://black.readthedocs.io/) for code formatting with a line length of 100:

```bash
black src/ tests/ examples/
```

### Import Sorting

We use [isort](https://pycqa.github.io/isort/) for consistent import ordering:

```bash
isort src/ tests/ examples/
```

### Linting

We use [flake8](https://flake8.pycqa.org/) for linting:

```bash
flake8 src/ tests/ examples/
```

### Type Checking

We encourage type hints and use [mypy](https://mypy.readthedocs.io/) for type checking:

```bash
mypy src/
```

### Run All Quality Checks

```bash
# Format code
black src/ tests/ examples/
isort src/ tests/ examples/

# Check code quality
flake8 src/ tests/ examples/
mypy src/
```

## Testing

### Running Tests

We use [pytest](https://docs.pytest.org/) for testing:

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=transformer --cov-report=html

# Run specific test file
pytest tests/test_transformer.py

# Run specific test function
pytest tests/test_transformer.py::test_transformer_model
```

### Writing Tests

- Place tests in the `tests/` directory
- Name test files as `test_*.py`
- Name test functions as `test_*`
- Use descriptive names that explain what is being tested
- Include docstrings explaining the test purpose
- Use fixtures for common setup code

Example:

```python
def test_attention_output_shape():
    """Test that attention mechanism produces correct output shape."""
    batch_size, n_heads, seq_len, d_k = 2, 4, 10, 64
    Q = torch.randn(batch_size, n_heads, seq_len, d_k)
    K = torch.randn(batch_size, n_heads, seq_len, d_k)
    V = torch.randn(batch_size, n_heads, seq_len, d_k)
    
    output, attn_weights = scaled_dot_product_attention(Q, K, V)
    
    assert output.shape == (batch_size, n_heads, seq_len, d_k)
    assert attn_weights.shape == (batch_size, n_heads, seq_len, seq_len)
```

## Pull Request Process

1. **Fork the Repository**: Create your own fork of the project
2. **Create a Branch**: Create a feature branch from `main`
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make Changes**: Implement your changes following the code style guidelines
4. **Add Tests**: Add tests for your changes
5. **Run Tests**: Ensure all tests pass
   ```bash
   pytest
   ```
6. **Format Code**: Run code formatters
   ```bash
   black src/ tests/ examples/
   isort src/ tests/ examples/
   ```
7. **Commit Changes**: Write clear, descriptive commit messages
   ```bash
   git commit -m "Add feature: description of what you added"
   ```
8. **Push to Fork**: Push your changes to your fork
   ```bash
   git push origin feature/your-feature-name
   ```
9. **Create Pull Request**: Open a PR against the main repository

### Pull Request Guidelines

- **Description**: Provide a clear description of what your PR does
- **Tests**: Ensure all tests pass
- **Documentation**: Update documentation if needed
- **Code Style**: Follow the project's code style
- **Commits**: Use meaningful commit messages
- **Small PRs**: Keep PRs focused on a single feature or fix

## Project Structure

```
transformer/
├── src/transformerkit/      # Main package source code
│   ├── __init__.py          # Package exports
│   ├── config.py            # Configuration
│   ├── attention.py         # Attention mechanisms
│   ├── components.py        # Core components
│   ├── encoder.py           # Encoder implementation
│   ├── decoder.py           # Decoder implementation
│   ├── model.py             # Complete transformer
│   └── utils.py             # Utility functions
├── tests/                   # Test files
├── examples/                # Example scripts
└── docs/                    # Documentation
```

## Documentation

- **Code Comments**: Add comments for complex logic
- **Docstrings**: Use Google-style docstrings for all functions and classes
- **Type Hints**: Add type hints to function signatures
- **README**: Update README.md if adding new features

### Docstring Example

```python
def create_transformer(config: TransformerConfig) -> Transformer:
    """
    Create a Transformer model from configuration.
    
    Args:
        config: TransformerConfig object with model hyperparameters
        
    Returns:
        Transformer model instance
        
    Example:
        >>> config = TransformerConfig(d_model=512, n_heads=8)
        >>> model = create_transformer(config)
    """
    return Transformer(config)
```

## Reporting Issues

When reporting issues, please include:

- **Description**: Clear description of the issue
- **Reproduction Steps**: Steps to reproduce the issue
- **Expected Behavior**: What you expected to happen
- **Actual Behavior**: What actually happened
- **Environment**: Python version, OS, PyTorch version
- **Code Example**: Minimal code to reproduce the issue (if applicable)

## Feature Requests

For feature requests, please:

- Check if the feature has already been requested
- Provide a clear description of the feature
- Explain the use case and benefits
- Include examples of how it would work

## Questions

If you have questions:

- Check the [README](README.md) and documentation
- Search existing issues
- Open a new issue with the "question" label

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

## Code of Conduct

- Be respectful and inclusive
- Welcome newcomers and help them learn
- Focus on constructive feedback
- Keep discussions professional

Thank you for contributing! 🎉
