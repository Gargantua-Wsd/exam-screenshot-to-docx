# Screenshot to DOCX

涓€涓潰鍚戠粍鍗风綉绔欐埅鍥剧殑鍥剧墖淇濈湡鍨?Word 鐢熸垚 skill銆傚畠鎶婇鐩埅鍥捐鎴愮嫭绔嬪浘鐗囷紝淇濈暀棰樺浘銆佸叕寮忓拰鍘熷瑙嗚甯冨眬锛屽苟鏍规嵁棰樼洰闀垮害鑷姩杩藉姞绛旈椤点€?
## 鏈湴杩愯

```powershell
python scripts/assemble.py --input .\example.jpg --output .\out
```

杈撳嚭鍖呮嫭锛?
- `exam_from_screenshot.docx`
- `question_images/`
- `question_boundaries.png`
- `processing_report.json`

濡傛灉鑷姩鍒囧壊涓嶇悊鎯筹紝鍙互鎸囧畾鍍忕礌杈圭晫锛?
```powershell
python scripts/assemble.py --input example.jpg --output out --split-mode manual --cuts 0,900,1800,2700
```

杩欐槸涓€涓浘鐗囦繚鐪熷伐鍏凤紝OCR 浠呯敤浜庤緟鍔╁垽鏂紝涓嶄細鐢ㄨ瘑鍒枃鏈浛鎹㈠師濮嬮鐩浘鐗囥€?
