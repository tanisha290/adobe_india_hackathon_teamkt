# Adobe India Hackathon - Connecting the Dots Challenge

## Overview

This repository contains solutions for both Round 1A (PDF Outline Extraction) and Round 1B (Persona-Driven Document Intelligence) of the Adobe India Hackathon. The solutions provide intelligent document analysis capabilities that extract structured information and provide contextually relevant insights based on user personas and job requirements.

## Challenge A: PDF Outline Extraction

Extracts structured outlines from PDF documents, identifying titles and headings (H1, H2, H3, H4) with their respective page numbers. The system uses **pure intelligent algorithms** with **no hardcoded logic**, making it truly general-purpose for any PDF structure.

## Approach

### 1. Title Extraction
- Analyzes the first page of the PDF to identify the document title
- Uses font size analysis to find the largest text elements
- Combines words with similar font sizes to reconstruct the complete title

### 2. Heading Detection
- **Pattern Matching**: Uses regex patterns to identify common heading formats (ALL CAPS, numbered headings, title case)
- **Keyword Recognition**: Identifies standard section keywords (Introduction, Conclusion, Abstract, etc.)
- **Font Analysis**: Analyzes font size, weight, and positioning to distinguish headings from body text
- **Contextual Analysis**: Considers text length, capitalization, and positioning on the page

### 3. Heading Classification (H1, H2, H3, H4)
- **K-means Clustering**: Groups headings by font size into distinct levels
- **Fallback Heuristics**: Uses simple threshold-based classification when clustering isn't suitable
- **Hierarchical Sorting**: Orders headings by page number and level for logical structure

### 4. Multi-language Support
- Handles various text encodings and character sets
- Supports documents with mixed languages
- Uses Unicode-aware text processing

## Models and Libraries Used

### Core Libraries
- **pdfplumber**: Advanced PDF text extraction with font and layout information
- **scikit-learn**: K-means clustering for heading level classification
- **numpy**: Numerical operations for clustering and analysis
- **re**: Regular expressions for pattern matching

### Key Features
- **Font Size Analysis**: Extracts and analyzes font sizes for heading classification
- **Positional Analysis**: Considers text positioning and layout
- **Pattern Recognition**: Multiple regex patterns for different heading styles
- **Robust Error Handling**: Graceful degradation for problematic PDFs

## Performance Characteristics

- **Execution Time**: < 10 seconds for 50-page PDFs
- **Model Size**: < 200MB (uses lightweight clustering)
- **Memory Usage**: Optimized for 16GB RAM systems
- **CPU Usage**: Efficient multi-core processing

## Building and Running

### Prerequisites
- Python 3.8+
- Required packages: pdfplumber, PyPDF2, numpy, scikit-learn

### Install Dependencies
```bash
pip install -r requirements.txt
```

### Run the Solution
```bash
python main.py
```

### Input/Output Structure
- **Input**: Place PDF files in the `input/` directory
- **Output**: JSON files will be generated in the `output/` directory
- **Format**: Each `filename.pdf` generates a corresponding `filename.json`

### Output Format
```json
{
  "title": "Document Title",
  "outline": [
    {
      "level": "H1",
      "text": "Introduction",
      "page": 1
    },
    {
      "level": "H2", 
      "text": "Background",
      "page": 2
    }
  ]
}
```

## Technical Implementation

### Key Algorithms
1. **Font Size Clustering**: K-means clustering to group headings by size
2. **Pattern Matching**: Multiple regex patterns for heading detection
3. **Contextual Analysis**: Position and layout-based heading identification
4. **Hierarchical Classification**: Multi-level heading classification system

### Error Handling
- Graceful handling of corrupted PDFs
- Fallback mechanisms for edge cases
- Robust text encoding support
- Memory-efficient processing for large documents

### Optimization Features
- Efficient PDF parsing with pdfplumber
- Optimized clustering algorithms
- Memory-conscious text processing
- Fast JSON serialization

## Testing

The solution has been tested with the provided test files and demonstrates intelligent extraction capabilities:

### Test Results
- **file01.pdf**: Application form with form field headings
- **file02.pdf**: Technical document with structured sections
- **file03.pdf**: RFP document with complex hierarchy
- **file04.pdf**: Educational pathway document
- **file05.pdf**: Event invitation with address information

### Test Commands
```bash
# Test general-purpose extraction
python test_general_purpose.py

# Process all PDFs
python main.py
```

## Constraints Compliance

✅ **No Hardcoded Logic**: Uses only intelligent algorithms  
✅ **No API Calls**: All processing is local  
✅ **Execution Time**: < 10 seconds for 50-page PDFs  
✅ **Model Size**: < 200MB  
✅ **Network**: No internet access required  
✅ **Architecture**: AMD64 compatible  
✅ **Runtime**: CPU-only processing  

## Solution Architecture

### Pure General-Purpose Approach
The solution uses **only intelligent algorithms** with **no hardcoded logic**:

1. **Intelligent Title Extraction**: Font size analysis and text reconstruction
2. **Pattern-Based Heading Detection**: Regex patterns and keyword matching
3. **Clustering-Based Classification**: K-means clustering for heading levels
4. **Contextual Filtering**: Removes headers/footers and noise

### Key Benefits
- **Universal Compatibility**: Works with any PDF structure and format
- **No Hardcoded Logic**: Fully compliant with hackathon rules
- **Intelligent Processing**: Adapts to different document types
- **Robust Performance**: Handles various document complexities

## Future Enhancements

- Enhanced multi-language support
- Improved heading context analysis
- Better handling of complex layouts
- Integration with semantic analysis
- Support for more heading levels (H5, H6)

---

## Challenge B: Persona-Driven Document Intelligence

Intelligently analyzes document collections based on specific persona requirements and job-to-be-done scenarios. The system extracts and prioritizes the most relevant sections from multiple documents, providing contextually relevant insights for different user types and tasks.

### Approach

#### 1. Persona and Job Analysis
- **Dynamic Keyword Extraction**: Analyzes persona descriptions and job requirements to extract relevant keywords
- **Domain-Specific Knowledge**: Pre-defined keyword mappings for common personas (researcher, student, analyst, manager, journalist, entrepreneur)
- **Task Understanding**: Identifies job-specific requirements (literature review, analysis, summary, preparation, research)

#### 2. Document Structure Extraction
- **Building on Challenge A**: Leverages the PDF outline extractor to identify document structure
- **Hierarchical Analysis**: Extracts sections with page-level granularity
- **Cross-Document Analysis**: Identifies patterns across document collections

#### 3. Content Relevance Scoring
- **TF-IDF Vectorization**: Converts document sections into vector representations
- **Cosine Similarity**: Calculates semantic relevance between content and requirements
- **Multi-Dimensional Scoring**: Combines semantic similarity with keyword matching
- **Hybrid Algorithm**: Weighted combination of multiple scoring methods

#### 4. Intelligent Ranking and Selection
- **Top-Section Selection**: Identifies the 20 most relevant sections across all documents
- **Subsection Analysis**: Extracts granular content with relevance scoring
- **Quality Filtering**: Ensures only high-quality, relevant content is included

### Models and Libraries Used

#### Core Libraries
- **pdfplumber**: Advanced PDF text extraction (from Challenge A)
- **scikit-learn**: TF-IDF vectorization and cosine similarity
- **numpy**: Numerical operations for scoring and ranking
- **spacy**: Advanced NLP processing capabilities

#### Key Features
- **Persona Adaptation**: Dynamic keyword extraction and scoring
- **Cross-Document Analysis**: Identifies relevant content across multiple documents
- **Contextual Intelligence**: Maintains document structure and relationships
- **Robust Error Handling**: Graceful degradation for problematic documents

### Performance Characteristics

- **Execution Time**: < 60 seconds for 3-5 documents
- **Model Size**: < 1GB (lightweight TF-IDF approach)
- **Memory Usage**: Optimized for 16GB RAM systems
- **CPU Usage**: Efficient multi-core processing

### Building and Running Challenge B

#### Prerequisites
- Docker with AMD64 support
- 8+ CPU cores recommended
- 16GB RAM recommended

#### Build the Docker Image
```bash
docker build --platform linux/amd64 -f Dockerfile.challenge_b -t persona-document-analyzer:latest .
```

#### Run the Solution
```bash
docker run --rm \
  -v $(pwd)/input:/app/input \
  -v $(pwd)/output:/app/output \
  --network none \
  persona-document-analyzer:latest
```

#### Input Configuration
Create a `config.json` file in the input directory:
```json
{
  "persona": "PhD Researcher in Computational Biology",
  "job_to_be_done": "Prepare a comprehensive literature review focusing on methodologies, datasets, and performance benchmarks"
}
```

#### Output Format
```json
{
  "metadata": {
    "input_documents": [...],
    "persona": "PhD Researcher in Computational Biology",
    "job_to_be_done": "Prepare a comprehensive literature review...",
    "processing_timestamp": "2024-01-01T12:00:00",
    "processing_time_seconds": 45.2
  },
  "extracted_sections": [
    {
      "document": "research_paper_1.pdf",
      "page": 3,
      "section_title": "Methodology",
      "importance_rank": 0.85
    }
  ],
  "sub_section_analysis": [
    {
      "document": "research_paper_1.pdf",
      "page": 3,
      "refined_text": "The experimental setup consisted of...",
      "relevance_score": 0.92
    }
  ]
}
```

### Technical Implementation

#### Key Algorithms
1. **TF-IDF Vectorization**: Document-to-vector conversion for similarity analysis
2. **Cosine Similarity**: Semantic relevance calculation
3. **Multi-Factor Scoring**: Weighted combination of relevance metrics
4. **Content Segmentation**: Paragraph-level analysis and extraction

#### Error Handling
- Graceful handling of corrupted PDFs
- Fallback scoring mechanisms for edge cases
- Robust text encoding support
- Memory-efficient processing for large document collections

#### Optimization Features
- Efficient TF-IDF computation
- Optimized similarity calculations
- Memory-conscious text processing
- Fast JSON serialization

### Constraints Compliance

✅ **Execution Time**: < 60 seconds for document collections  
✅ **Model Size**: < 1GB  
✅ **Network**: No internet access required  
✅ **Architecture**: AMD64 compatible  
✅ **Runtime**: CPU-only processing  

### Innovation Highlights

1. **Adaptive Persona Understanding**: Dynamic keyword extraction from persona descriptions
2. **Intelligent Content Prioritization**: Multi-dimensional scoring algorithm
3. **Cross-Document Analysis**: Identifies patterns across document collections
4. **Contextual Intelligence**: Maintains document structure and relationships

### Future Enhancements

- Advanced transformer-based semantic understanding
- Named entity recognition for better context
- Learning-based persona adaptation
- Real-time relevance updates
- Enhanced multi-language support 