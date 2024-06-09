from PIL import Image, ImageDraw, ImageFont

# Load the images
img1_path = "/mnt/data/file-IRYJNKlBvZ4FtQkVrFQmpmCA"
img2_path = "/mnt/data/file-WBTdMrGj2NeWS5YMIZZ0P2vS"
img3_path = "/mnt/data/file-OsWw8DRD3H1dNxIrovbP6YFv"

img1 = Image.open(img1_path)
img2 = Image.open(img2_path)
img3 = Image.open(img3_path)

# Create a new flyer image
flyer_width, flyer_height = 800, 1200
flyer = Image.new("RGB", (flyer_width, flyer_height), (255, 255, 255))
draw = ImageDraw.Draw(flyer)

# Define geometric shapes (circles)
shape_size = 250
shapes = [
    (50, 50, 50 + shape_size, 50 + shape_size),
    (275, 50, 275 + shape_size, 50 + shape_size),
    (500, 50, 500 + shape_size, 500 + shape_size)
]

# Resize images to fit into shapes
img1 = img1.resize((shape_size, shape_size))
img2 = img2.resize((shape_size, shape_size))
img3 = img3.resize((shape_size, shape_size))

# Create circular masks
mask = Image.new("L", (shape_size, shape_size), 0)
draw_mask = ImageDraw.Draw(mask)
draw_mask.ellipse((0, 0, shape_size, shape_size), fill=255)

# Paste images into flyer with circular masks
flyer.paste(img1, shapes[0][:2], mask)
flyer.paste(img2, shapes[1][:2], mask)
flyer.paste(img3, shapes[2][:2], mask)

# Add text
font_path = "/usr/share/fonts/truetype/dejavu/DejaVuSans-Bold.ttf"
title_font = ImageFont.truetype(font_path, 50)
body_font = ImageFont.truetype(font_path, 30)
small_font = ImageFont.truetype(font_path, 20)

# Title
title_text = "Tennis Coaching for Kids (Ages 8-13)"
draw.text((50, 350), title_text, font=title_font, fill="black")

# Description
description_text = (
    "Umair Dewan, an experienced and dedicated tennis coach, is now offering\n"
    "specialized tennis training for kids aged 8 to 13. Whether your child is just\n"
    "starting out or looking to improve their skills, Umair's coaching will help\n"
    "them develop their game and love for tennis in a fun and supportive\n"
    "environment. Don't miss this opportunity to give your child the gift of a\n"
    "healthy and active lifestyle through tennis!"
)
draw.text((50, 450), description_text, font=body_font, fill="black")

# Contact information
contact_text = "Call for more information: 248-847-5280"
draw.text((50, 750), contact_text, font=small_font, fill="black")

# Save the flyer
flyer_path = "/mnt/data/tennis_flyer_final.png"
flyer.save(flyer_path)

flyer_path
