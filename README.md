# 🎓 Learn AWS - FCJ 2025

> Trang giới thiệu dự án học AWS của bạn trong chương trình AWS Foundation Cloud Journey 2025

**Trang web**: [https://nguyenkethang.github.io/Learn-AWS--FCJ-2025/](https://nguyenkethang.github.io/Learn-AWS--FCJ-2025/)

## 📖 Giới thiệu

Dự án này là báo cáo thực tập và tài liệu học tập AWS của bạn, bao gồm các bài học, workshop, và blog đã dịch trong quá trình tham gia AWS Foundation Cloud Journey 2025.

## 📁 Cấu trúc dự án

```
fcj-workshop-template-main/
├── content/                            # 📝 Nội dung chính
│   ├── 1-Worklog/                     # 📅 Nhật ký công việc hàng tuần
│   ├── 2-Proposal/                    # 📋 Đề xuất dự án
│   ├── 3-BlogsTranslated/             # 📰 Bài blog đã dịch
│   ├── 4-EventParticipated/           # 🎉 Sự kiện tham gia
│   ├── 5-Workshop/                    # 🔧 Workshop thực hành
│   ├── 6-Self-evaluation/             # 📊 Tự đánh giá
│   └── 7-Feedback/                    # 💬 Phản hồi & suy ngẫm
├── layouts/
│   ├── partials/                      # Custom HTML partials
│   │   ├── custom-footer.html
│   │   ├── logo.html
│   │   └── menu-footer.html
│   └── shortcodes/                    # Custom Hugo shortcodes
│       ├── ghcontributors.html
│       ├── tab.html
│       └── tabs.html
├── static/                            # Static assets (images, fonts, CSS)
│   ├── css/
│   │   ├── theme-mine.css
│   │   └── theme-workshop.css
│   ├── fonts/
│   ├── images/
│   │   ├── 2-Proposal/                # Architecture diagrams
│   │   ├── 5-Workshop/                # Workshop screenshots
│   │   ├── avatar.png
│   │   └── favicon.png
│   └── AWS_Logo.svg
├── themes/
│   └── hugo-theme-learn/              # Hugo Learn theme
├── public/                            # 🚀 Generated static site (auto-built)
├── config.toml                        # Hugo configuration
└── README.md                          # This file
```

### 📊 Thống kê nội dung

- **Weekly Logs**: 12 tuần báo cáo công việc chi tiết
- **Translated Blogs**: 6 bài viết kỹ thuật AWS
- **Events**: 2 sự kiện cộng đồng AWS đã tham gia
- **Workshop**: Lab thực hành hoàn chỉnh với S3 VPC Endpoints
- **Languages**: Hỗ trợ song ngữ đầy đủ (Tiếng Anh & Tiếng Việt)

## 🛠️ Tech Stack

- **Static Site Generator**: Hugo v0.134.3 (Extended)
- **Theme**: [Hugo Learn Theme](https://github.com/matcornic/hugo-theme-learn)
- **Deployment**: GitHub Pages via GitHub Actions
- **Languages**: Vietnamese & English

## 🚢 Deployment

Website tự động deploy khi push lên branch `main`:

1. GitHub Actions chạy workflow
2. Build Hugo site với `hugo --minify`
3. Deploy lên GitHub Pages

Xem deployment status tại [Actions tab](https://github.com/nguyenkethang/Learn-AWS--FCJ-2025/actions)

## 🔧 Configuration

Chỉnh sửa `config.toml` để thay đổi:

- Base URL
- Site title
- Theme variant
- Menu shortcuts
- Language settings

## 📚 Workshop Content



## 👤 Author

**Email**: nguyenkethang111@gmail.com

## 🔗 Links

- [AWS Study Group Facebook](https://www.facebook.com/groups/awsstudygroupfcj/)
- [Hugo Documentation](https://gohugo.io/documentation/)
- [Hugo Learn Theme Docs](https://learn.netlify.app/en/)

## 📄 License

This project is for educational purposes as part of AWS FCJ 2025 internship program.
