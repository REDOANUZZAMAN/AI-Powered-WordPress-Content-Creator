# ✍️ AI-Powered WordPress Content Creator

An intelligent n8n workflow that automatically generates SEO-optimized WordPress articles with AI. Creates complete blog posts with structured content, featured images, and proper formatting using OpenAI's GPT-4 and DALL-E.

![Status](https://img.shields.io/badge/status-active-success.svg)
![n8n](https://img.shields.io/badge/n8n-workflow-FF6D5A?style=flat&logo=n8n&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white)
![WordPress](https://img.shields.io/badge/WordPress-21759B?style=flat&logo=wordpress&logoColor=white)

## ✨ Features

- **User-Friendly Form** - Simple web form for triggering post creation
- **AI-Powered Structure** - GPT-4 generates title, subtitle, chapters, and introduction
- **Wikipedia Integration** - Enriches content with verified information
- **Multi-Chapter Support** - Creates articles with 1-10 customizable chapters
- **Smart Content Flow** - AI ensures logical progression between chapters
- **DALL-E Image Generation** - Automatically creates photographic featured images
- **Data Validation** - Checks content consistency before posting
- **WordPress Integration** - Posts as draft with featured image attached
- **HTML Formatting** - Properly formatted with bold, italic, and lists
- **SEO-Friendly** - Optimized structure and keyword integration

## 🎯 Use Case

Perfect for content creators, bloggers, and marketers who want to:
- Generate comprehensive blog posts quickly
- Maintain consistent article structure
- Create SEO-optimized content at scale
- Automatically generate featured images
- Save time on research and writing
- Produce professional WordPress drafts

## 🚀 Quick Start

### 1. Import Workflow

```bash
# In n8n interface:
# 1. Go to Workflows → Import from File
# 2. Upload "Write a WordPress post with AI.json"
# 3. Workflow will be imported with all nodes
```

### 2. Configure Credentials

Set up authentication for each service:

| Service | Auth Type | Required Access |
|---------|-----------|----------------|
| OpenAI API | API Key | GPT-4, DALL-E 3 |
| WordPress | Application Password | Posts, Media |

### 3. Update WordPress URL

```javascript
// Open "Settings" node
// Update this field:
wordpress_url: "https://your-wordpress-site.com/"
```

### 4. Configure WordPress Credentials

```bash
# In WordPress admin:
# 1. Go to Users → Profile
# 2. Scroll to "Application Passwords"
# 3. Create new application password
# 4. Add to n8n WordPress credential
```

### 5. Activate Webhook

```bash
# 1. Open "Form" node
# 2. Click "Test workflow"
# 3. Copy the Production URL
# 4. Share with your team or embed in website
```

### 6. Test the Workflow

```bash
# 1. Open the form URL in browser
# 2. Fill in:
#    - Keywords: "artificial intelligence, machine learning"
#    - Number of chapters: 5
#    - Max words count: 1000
# 3. Submit and wait for confirmation
# 4. Check WordPress for draft post
```

## 📁 Workflow Structure

```
Form Trigger
    ↓
Settings Configuration
    ↓
AI Article Structure (GPT-4 + Wikipedia)
    ↓
Data Consistency Check
    ↓
    ├─ Valid → Continue
    └─ Invalid → Error Response
    ↓
Split Chapters
    ↓
Generate Chapter Content (GPT-4)
    ↓
Merge & Format Content
    ↓
Post Draft to WordPress
    ↓
Generate Featured Image (DALL-E)
    ↓
Upload Image to WordPress
    ↓
Attach Featured Image
    ↓
Success Response
```

## 🎨 Form Parameters

### Keywords (Required)
```
Example: "digital marketing, SEO, content strategy"
- Comma-separated topics
- Used for content generation
- Influences article direction
```

### Number of Chapters (Required)
```
Options: 1-10
- Determines article structure
- Each chapter is AI-generated
- Chapters flow logically
```

### Max Words Count (Required)
```
Example: 1500
- Total article length
- Distributed across chapters
- ~120 words for intro/conclusions
- Remaining divided among chapters
```

## 🔄 Content Generation Process

### 1. Article Structure Creation
```javascript
GPT-4 generates:
- Title (SEO-optimized)
- Subtitle
- Introduction (~60 words)
- Chapter titles and prompts
- Conclusions (~60 words)
- Image prompt for DALL-E
```

### 2. Wikipedia Research
```javascript
- AI searches Wikipedia for facts
- Verifies information accuracy
- Enriches content with data
- No mention of source in article
```

### 3. Chapter Generation
```javascript
For each chapter:
- Receives dedicated prompt
- Considers previous chapter context
- Maintains logical flow
- Uses HTML formatting
- Target length calculated automatically
```

### 4. Content Assembly
```javascript
Final article structure:
<introduction>
<strong>Chapter 1 Title</strong>
Chapter 1 content...
<strong>Chapter 2 Title</strong>
Chapter 2 content...
...
<strong>Conclusions</strong>
Conclusions content...
```

### 5. Image Generation
```javascript
DALL-E 3 creates:
- Photographic style
- Based on article title + custom prompt
- Size: 1792x1024 (landscape)
- Natural style (realistic)
- Sigma 85mm f/1.4 aesthetic
```

## 🛠️ Technologies Used

- **[n8n](https://n8n.io/)** - Workflow automation platform
- **[OpenAI GPT-4](https://openai.com/)** - Content generation
- **[OpenAI DALL-E 3](https://openai.com/)** - Image generation
- **[Wikipedia API](https://www.mediawiki.org/wiki/API)** - Fact verification
- **[WordPress REST API](https://developer.wordpress.org/rest-api/)** - Content publishing

## 📊 Workflow Nodes Overview

| Node | Type | Purpose |
|------|------|---------|
| Form | Webhook Trigger | User input collection |
| Settings | Data Processing | Parameter configuration |
| Create post title and structure | AI (GPT-4) | Article structure generation |
| Wikipedia | AI Tool | Information research |
| Check data consistency | Conditional | Validate AI output |
| Split out chapters | Data Processing | Separate chapters |
| Create chapters text | AI (GPT-4) | Chapter content generation |
| Merge chapters | Data Processing | Combine content |
| Final article text | Code | HTML formatting |
| Post on WordPress | API | Create draft post |
| Generate featured image | AI (DALL-E) | Image creation |
| Upload media | HTTP Request | Image upload |
| Set image ID for post | HTTP Request | Image attachment |
| Respond: Success/Error | Webhook Response | User feedback |

## 🎨 Customization

### Adjust GPT-4 Model

```javascript
// In "Create post title and structure" node
modelId: "gpt-4-1106-preview"  // Change to gpt-4, gpt-4-turbo, etc.

// In "Create chapters text" node
modelId: "gpt-4-0125-preview"  // Change model version
```

### Modify Content Guidelines

```javascript
// Edit system prompts in OpenAI nodes
// For example, change:
"- Go deep in the topic you treat"
// To:
"- Keep explanations beginner-friendly"
```

### Change Image Style

```javascript
// In "Generate featured image" node
prompt: "...photography, realistic, sigma 85mm f/1.4"
// Change to:
prompt: "...digital art, vibrant colors, modern illustration"

// Or adjust size:
options.size: "1024x1024"  // Square format
```

### Add Custom HTML Tags

```javascript
// In "Final article text" node
// Modify the article assembly code:
article += "<h2>" + item.json.title + "</h2>";  // Use H2 instead of strong
article += "<div class='chapter'>" + item.json.message.content + "</div>";
```

### Change WordPress Post Status

```javascript
// In "Post on Wordpress" node
status: "draft"  // Change to "publish", "pending", "private"
```

### Add Post Categories/Tags

```javascript
// In "Post on Wordpress" node
additionalFields: {
  categories: [1, 5],  // Category IDs
  tags: [10, 15, 20],  // Tag IDs
  status: "draft"
}
```

## 🐛 Troubleshooting

### Form Not Loading

```bash
# Check these items:
1. Workflow is Active
2. Form node webhook URL is accessible
3. No firewall blocking n8n instance
4. Test with: curl -X POST [webhook-url]
```

### AI Returns Incomplete Data

```bash
# Common causes:
1. Token limit reached (increase maxTokens)
2. Complex topics requiring more processing
3. Network timeout with OpenAI
# Solution: Check "Data consistency" node logs
```

### WordPress API Errors

```bash
# Verify:
1. Application Password is correct
2. WordPress user has "author" or higher role
3. REST API is enabled (not blocked by security plugin)
4. URL format: https://site.com (no trailing slash)
```

### Image Upload Fails

```bash
# Check:
1. WordPress media upload permissions
2. PHP upload_max_filesize setting
3. DALL-E image was successfully generated
4. Content-Disposition header format
```

### Chapters Don't Flow Logically

```bash
# Improvements:
1. Increase maxTokens for better context
2. Use more specific keywords
3. Adjust chapter prompts in GPT-4 output
4. Review "Create chapters text" prompt logic
```

### Wikipedia Tool Not Working

```bash
# Verify:
1. Wikipedia API is accessible
2. Keywords match Wikipedia article titles
3. AI tool is properly connected
4. Check n8n logs for API errors
```

## 📝 Best Practices

### 1. Keyword Selection
- Use 2-4 related keywords
- Be specific (not just "technology")
- Include target SEO terms
- Separate with commas

### 2. Chapter Planning
- 3-5 chapters for 1000-word articles
- 5-7 chapters for 1500+ word articles
- Fewer chapters = more depth per topic
- More chapters = broader coverage

### 3. Word Count Guidelines
- Minimum: 500 words (3 chapters)
- Sweet spot: 1000-1500 words (5 chapters)
- Maximum: 3000+ words (8-10 chapters)
- Consider target audience attention span

### 4. Image Prompts
- Let AI generate based on title
- AI considers article context
- Photographic style works best
- Landscape format for featured images

### 5. Quality Control
- Always review draft before publishing
- Check factual accuracy
- Verify HTML formatting
- Test internal/external links
- Optimize meta description manually

### 6. Performance Optimization
- Don't exceed 2048 maxTokens per node
- Use appropriate GPT-4 model version
- Consider rate limits on OpenAI API
- Monitor execution times

## 🔒 Security Considerations

- Store OpenAI API keys securely in n8n
- Use WordPress Application Passwords (not main password)
- Restrict form access with authentication if needed
- Enable HTTPS for webhook URLs
- Review generated content before publishing
- Monitor OpenAI API usage and costs
- Regularly rotate WordPress application passwords

## 📈 Performance Metrics

Track these KPIs:
- Average execution time (expect 3-5 minutes)
- Content generation success rate
- Image generation success rate
- WordPress posting success rate
- Average article word count accuracy
- User form completion rate

## 💰 Cost Considerations

### OpenAI API Costs (Approximate)
```
GPT-4 (structure): ~$0.10-0.20 per article
GPT-4 (chapters): ~$0.30-0.60 per article (5 chapters)
DALL-E 3: ~$0.04 per image (1792x1024)
Total: ~$0.50-1.00 per article
```

### Tips to Reduce Costs
- Use GPT-3.5-Turbo for less critical content
- Reduce maxTokens if appropriate
- Batch process multiple articles
- Cache frequently used prompts

## 🌐 Browser Requirements

Form interface works on:
- ✅ Chrome (recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Edge
- ✅ Mobile browsers

## 💡 Enhancement Ideas

- [ ] Add multiple language support
- [ ] Integrate with SEO analysis tools
- [ ] Add content tone selector (formal, casual, technical)
- [ ] Include internal linking suggestions
- [ ] Generate meta descriptions
- [ ] Create social media post versions
- [ ] Add plagiarism checking
- [ ] Schedule post publication
- [ ] A/B test different title variations
- [ ] Generate video scripts from articles
- [ ] Add voice-over audio generation
- [ ] Create infographics from content

## 📄 License

This workflow is open source and available under the [MIT License](LICENSE).

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add multilingual support'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 👨‍💻 Author

**Redoanuzzaman**
- GitHub: [@redoanuzzaman](https://github.com/redoanuzzaman)
- Email: redoanuzzaman707@gmail.com
- Website: [redoan.dev](https://redoan.dev)

## 🙏 Acknowledgments

- OpenAI for GPT-4 and DALL-E 3 APIs
- n8n community for workflow automation patterns
- Wikipedia for knowledge enrichment
- WordPress REST API documentation

## 💖 Show Your Support

Give a ⭐️ if this workflow helped automate your content creation!

## 📞 Support

Need help?
1. Check [n8n Documentation](https://docs.n8n.io/)
2. Visit [OpenAI API Documentation](https://platform.openai.com/docs)
3. Review [WordPress REST API Handbook](https://developer.wordpress.org/rest-api/)
4. Open an issue in this repository

---

Made with 🤖 and AI

**Last Updated:** October 2025
