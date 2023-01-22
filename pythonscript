from io import StringIO
from pdfminer.pdfinterp import PDFResourceManager, PDFPageInterpreter
from pdfminer.converter import TextConverter
from pdfminer.layout import LAParams
from pdfminer.pdfpage import PDFPage
from gtts import gTTS
import os

def pdf_to_text(pdf_file):
    rsrcmgr = PDFResourceManager()
    retstr = StringIO()
    codec = 'utf-8'
    laparams = LAParams()
    device = TextConverter(rsrcmgr, retstr, codec=codec, laparams=laparams)
    interpreter = PDFPageInterpreter(rsrcmgr, device)
    password = ""
    maxpages = 0
    caching = True
    pagenos=set()
    for page in PDFPage.get_pages(pdf_file, pagenos, maxpages=maxpages, password=password,caching=caching, check_extractable=True):
        interpreter.process_page(page)
    device.close()
    text = retstr.getvalue()
    retstr.close()
    return text

with open("example.pdf", "rb") as f:
    text = pdf_to_text(f)
    # Use gTTS to convert the text to an audio file
    tts = gTTS(text)
    audio_file = 'example.mp3'
    tts.save(audio_file)
    # Play the audio file using the default media player
    os.system("start " + audio_file)
