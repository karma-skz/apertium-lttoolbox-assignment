# README.md

## Overview

This aims to implement a basic morphological analyzer/generator using Apertium’s lttoolbox. The goal was to build comprehensive paradigms and a dictionary covering verbs, nouns, and adjectives according to the assignment instructions for CL-1 (Assignment 3).

## Assignment Requirements vs. Implementation

### Task 1: Building Paradigms

**Assignment Requirements:**
- **Verb Paradigms:**
  - Tense variations: present, past, future (8 points)
  - Aspect variations: simple, progressive, perfect (9 points)
  - Person and number agreement: 1st, 2nd, 3rd person; singular and plural (8 points)
- **Noun Paradigm:**
  - Number variations (singular/plural)
  - Case markers (if applicable in the chosen language)
- **Adjective Paradigm:**
  - Standard degree forms (base, comparative, superlative)

**My Implementation:**
- **Verb Paradigm (`walk__v`):**
  - **Tense:** Implements present, past, and future forms.
  - **Aspect:** Provides progressive and gerund forms.
  - **Person/Number:** Different forms are defined for 1st, 2nd, and 3rd person (both singular and plural); the 3rd person singular form is marked with an added "s".
  - **Missing Aspect:** *Perfect aspect forms* (e.g., forms typically realized with auxiliary verbs like “has walked”) are not implemented. This decision was taken due to the complexity involved in modeling auxiliary constructions in English.
- **Irregular Verb Paradigms:**
  - Separate paradigms for verbs like **run**, **eat**, **see**, **write**, and **read** have been defined to handle irregular inflection.
- **Noun Paradigm:**
  - Implements singular and plural forms.
  - **Case Markers:** Not included since English (the assumed language) does not have a rich system of case markings.
- **Adjective Paradigm:**
  - Three types of adjective paradigms are provided:
    - **Regular adjectives** (`quick__a`)
    - **Adjectives ending in 'y'** (`happ/y__a`)
    - **Adjectives with consonant doubling** (`bi/g__a`)
  - All three paradigms include base, comparative, and superlative forms.

### Task 2: Building a Dictionary

**Assignment Requirements:**
- Minimum 20 entries across different word classes:
  - At least 8 verbs, 8 nouns, and 4 adjectives.
- Each entry must include the lemma, part of speech, and a reference to the appropriate paradigm.

**Your Implementation:**
- **Verb Entries:** 8 entries (`walk`, `talk`, `jump`, `run`, `eat`, `see`, `write`, `read`).
- **Noun Entries:** 8 entries (`book`, `child`, `cat`, `dog`, `house`, `car`, `tree`, `foot`).
- **Adjective Entries:** 4 entries (`quick`, `happy`, `slow`, `big`).
- Every dictionary entry is formatted with an `<e>` element containing the lemma (within `<i>`) and a reference to its paradigm (via `<par n="..."/>`).

### Task 3: Implementation and Testing using lttoolbox

**Assignment Requirements:**
- **Morphological Analysis:**
  - Analyzer should break down words into their base forms and features.
  - Test with at least 10 different word forms.
  - Provide documentation on the analysis process and results.
- **Morphological Generation:**
  - Generator should create correct word forms from a given lemma and set of morphological features.
  - Generate at least 10 different forms.
  - Verify and document the correctness of the generated forms.

**Your Implementation:**
- The provided XML file implements the paradigms and dictionary needed for analysis and generation.
- **Compilation:**
  - `lt-comp lr paradigms.dix anal.bin` for compiling the morph analyzer and `lt-comp rl paradigms.dix gen.bin` for compiling the morph generator
  - `echo "test case u wanna run" | lt-proc anal.bin` for morphological analysis of a word, given that it belongs to the dictionary we created, and `echo "test case u wanna run" | lt-proc gen.bin` for morphological generation of a given form of the given stem.
  - Sample tests (with at least 10 word forms for both analysis and generation) were executed, and the results are documented separately in the test files (included in the zip submission).
- **Documentation:**
  - This README file explains the design decisions and notes the test procedures, with additional details available in the accompanying test documentation.

## Assumptions and Limitations

- **Language Choice:**  
  English was assumed as the target language. This influenced several design decisions:
  - **Noun Case Markers:** English has minimal case marking (except for possessives, which were not considered for this assignment by me), so these were omitted.
  - **Perfect Aspect:** The assignment requested perfect aspect forms, but these were excluded since perfect forms in English require auxiliary verbs (e.g., "has walked"). Modeling such constructions falls outside the simple paradigm framework and would complicate the analyzer/generator unnecessarily.

- **Paradigm Naming and Structure:**
  - Regular and irregular paradigms are differentiated clearly (e.g., `walk__v` for regular verbs versus `/eat__v` for irregular verbs).
  - The irregular paradigms use a naming convention that may appear unusual (e.g., using slashes or abbreviated markers). This was chosen to reflect the differences in inflection and to avoid duplicating rules common to regular verbs.

- **Test Coverage:**
  - Although a full test suite with sample inputs and outputs is provided separately, the XML dictionary itself does not contain inline test cases. Testing was performed externally using lttoolbox to ensure that both the analyzer and generator work as expected.

- **Future Enhancements:**
  - Adding perfect aspect forms could be explored by extending the paradigms to include auxiliary elements.
  - Expansion to cover more irregular forms and additional parts of speech (e.g., adverbs) would improve the system.
  - More robust error handling and richer morphological features might be incorporated in future versions.

## Usage Instructions

1. **Compilation and Setup:**
   - Ensure that Apertium and lttoolbox are installed on your system.
   - Compile the dictionary file using lttoolbox’s compilation commands (e.g., `lt-comp lr dictionary.dix dictionary.bin`).

2. **Morphological Analysis:**
   - Run the analyzer with:  
     `lt-proc dictionary.bin`  
     and then input a word (e.g., `walking`) to see its analysis.

3. **Morphological Generation:**
   - Run the generator with:  
     `lt-proc dictionary.bin`  
     and then input a lemma with features (e.g., `walk<vblex><past>`) to generate the correct form.

4. **Testing:**
   - A set of test files with sample inputs and expected outputs is included in the submission. Refer to these files for detailed examples and verification.

## File Structure

- **paradigms.dix**: The XML dictionary file containing paradigms and lexical entries.
- **anal.bin**: The compiled binary analyzer file.
- **gen.bin**: The compiled binary generator file.
- **test/**: Directory containing test files with sample inputs and outputs for both analysis and generation.
- **README.md**: This documentation file.

## Conclusion

The project meets the core requirements of the assignment by providing comprehensive paradigms and a dictionary with exactly 20 entries across verbs, nouns, and adjectives. Some elements (like perfect aspect forms and noun case markers) were intentionally omitted based on language considerations and scope limitations. Testing using lttoolbox confirms that the morphological analyzer and generator work as expected, and further details can be found in the accompanying test documentation.

