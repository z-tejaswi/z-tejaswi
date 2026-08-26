

<div align="center">

<table>
<tr>
<td valign="top"><img src="./avi-ascii.svg" width="370" alt="ASCII portrait" /></td>
<td valign="top"><img src="./info-card.svg" width="490" alt="Experience, stack, highlights" /></td>
</tr>
</table>

<img src="./contrib-heatmap.svg" width="860" alt="GitHub contribution graph" />

</div>

---

```
PROMPT.md                    a paste-into-Claude-Code prompt that drives it all
profile-README-template.md   the README that goes on your profile
requirements-local.txt       deps for the one-time local image prep
scripts/
  prep_photo.py              rembg background removal + CLAHE contrast (run once)
  make_ascii_svg.py          photo  -> typing monochrome ASCII portrait
  make_info_card.py          your experience/stack -> neofetch info panel  <- EDIT
  fetch_contributions.py     scrapes your real contributions (no auth)
  render_heatmap_svg.py      contributions -> animated box graph
  requirements.txt           deps the daily workflow needs
.github/workflows/
  update-profile-art.yml     refreshes the graph every day, automatically
```



```bash
# 0. deps
pip install -r requirements-local.txt        # local prep
pip install -r scripts/requirements.txt      # scraper

# 1. portrait  (STATIC=1 shows the final frame; drop it for the animated file)
python scripts/prep_photo.py path/to/your-photo.jpg source-prepped.png
python scripts/make_ascii_svg.py              # -> avi-ascii.svg

# 2. info panel  (edit the ROWS + HOST at the top of the script first)
python scripts/make_info_card.py              # -> info-card.svg

# 3. contribution graph
GH_PROFILE_USER=YOUR_USERNAME python scripts/fetch_contributions.py
python scripts/render_heatmap_svg.py          # -> contrib-heatmap.svg

# 4. README
cp profile-README-template.md README.md       # then fill in name / tagline / links
```



