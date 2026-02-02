# ACF Local JSON Skill

Agents skills to generate complete Advanced Custom Fields (ACF) Local JSON configurations for WordPress from visual designs, images, or HTML structures. This skill helps AI agents create ACF custom field schemas accurately and consistently.

## What This Skill Does

This skill enables AI agents to:

- **Analyze visual designs** (images, mockups, screenshots) and convert them into ACF configurations
- **Convert HTML structures** into appropriate ACF field groups
- **Generate valid JSON** ready to use with ACF Pro Local JSON
- **Detect complex patterns** like repeaters, flexible content, clone fields, and relationships
- **Apply best practices** automatically (semantic names, unique keys, correct structure)

## Installation

### Claude Code / Cursor / Copilot

```bash
npx skills add JoseCortezz25/local-json-acf-skill
```

### Manual Installation

```bash
# Clone the repository
git clone https://github.com/JoseCortezz25/local-json-acf-skill.git

# Copy the skill to your skills directory
cp -r local-json-acf-skill/skills/SKILL.md ~/.claude/skills/acf-local-json.md

# or for Cursor:
cp local-json-acf-skill/skills/SKILL.md ~/.cursor/skills/acf-local-json.md
```

1. Download the `SKILL.md` file from the `skills/` directory
2. Copy it to your skills directory:
   - **Claude Code**: `~/.claude/skills/`
   - **Cursor**: `~/.cursor/skills/` or `.cursor/skills/` in your project
   - **OpenCode**: `~/.opencode/skills/` or `.opencode/skills/` in your project

### Direct Download

Download the `SKILL.md` file directly from the `skills/` directory and save it to your project or skills directory.

## Project Structure

```
local-json-acf/
├── skills/
│   ├── SKILL.md                    # Main skill file
│   ├── assets/                     # Example templates
│   │   ├── template-hero-section.json
│   │   ├── template-card-repeater.json
│   │   └── template-page.json
│   ├── references/                 # Reference documentation
│   │   ├── clone-fields.md
│   │   ├── conditional-logic.md
│   │   ├── custom-types.md
│   │   └── relationships.md
│   └── scripts/                   # Utilities
│       └── generate_keys.py
└── README.md
```

## Key Features

### Automatic Field Type Detection

The skill automatically identifies appropriate ACF field types:

- **Text inputs/headings** → `text`, `textarea`, `wysiwyg`
- **Images** → `image` (or `gallery` for multiple)
- **Repeating sections** → `repeater` or `flexible_content`
- **Toggles/checkboxes** → `true_false` or `button_group`
- **Dropdowns** → `select` or `radio`
- **Dates** → `date_picker` or `date_time_picker`
- **Links** → `link` or `url`
- **Colors** → `color_picker`
- **Files** → `file`

### Unique Key Generation

The skill automatically generates unique keys following ACF conventions:

- **Group keys**: `group_` + descriptive_name + hash
- **Field keys**: `field_` + descriptive_name + hash
- **Layout keys**: `layout_` + layout_name + hash

### Advanced Features Support

- ✅ **Repeaters** - Repeating fields with sub-fields
- ✅ **Flexible Content** - Pages with multiple layouts
- ✅ **Clone Fields** - Reuse field groups
- ✅ **Conditional Logic** - Conditional fields based on other fields
- ✅ **Relationships** - Bidirectional relationships between posts
- ✅ **Custom Field Types** - Custom field types

## Main Usage

In your prompt, reference the skill:
```
Using the ACF Local JSON skill, generate the ACF fields for this design image:
[attach image]
```

## Usage Examples

### Generate Fields from an Image

```
Using the ACF Local JSON skill, analyze this hero section image and generate 
the necessary ACF fields. The image shows:
- Main title
- Subtitle
- CTA button
- Background image

[attach image]
```

### Convert HTML to ACF

```
Using the ACF Local JSON skill, analyze this HTML structure and generate 
the ACF Local JSON. Connect it dynamically without hardcoded values:

<div class="hero">
  <h1>Welcome to Our Platform</h1>
  <p>Build amazing websites with our tools</p>
  <a href="/signup" class="btn-primary">Get Started</a>
  <img src="/wp-content/uploads/2024/hero-bg.jpg" alt="Hero Background">
</div>
```

The skill generates the JSON and you connect it in your template:

```php
<div class="hero">
  <h1><?php echo esc_html(get_field('hero_title')); ?></h1>
  <p><?php echo esc_html(get_field('hero_subtitle')); ?></p>
  <?php $cta = get_field('hero_cta'); ?>
  <a href="<?php echo esc_url($cta['url']); ?>" class="btn-primary">
    <?php echo esc_html($cta['title']); ?>
  </a>
  <?php $bg = get_field('hero_background'); ?>
  <img src="<?php echo esc_url($bg['url']); ?>" alt="<?php echo esc_attr($bg['alt']); ?>">
</div>
```

### Create Complete Page

```
Generate a page with flexible content that includes these layouts:
- Hero section
- Features grid (3 columns)
- Testimonials carousel
- CTA section
```

### Generate Complex Repeater

```
Create a repeater for service cards with:
- Title
- Description
- Icon (image)
- Link
- Customizable background color
```

## What You Get

When an AI agent uses this skill, it will generate:

- ✅ **Valid JSON** ready to save in `acf-json/group_[name].json`
- ✅ **Unique keys** following ACF conventions
- ✅ **Correct structure** with all required fields
- ✅ **Semantic names** that reflect the content purpose
- ✅ **Best practices** applied automatically
- ✅ **Full support** for advanced ACF Pro features

## Requirements

- WordPress with ACF Pro installed
- ACF Pro Local JSON enabled (recommended configuration)
- Basic knowledge of WordPress and ACF (to use the generated JSON)

## Contributing

Want to improve this skill? Contributions are welcome:

1. Add new templates in `skills/assets/`
2. Improve documentation in `skills/references/`
3. Update `SKILL.md` with new capabilities
4. Open a PR with your improvements

---

**Note**: This skill is designed to work with ACF Pro. Some features like Flexible Content and Clone Fields require ACF Pro.
