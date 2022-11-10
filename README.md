- 👋 Hi, I’m @VaibhavDubey-AU
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
VaibhavDubey-AU/VaibhavDubey-AU is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np\n",
    "from PIL import ImageGrab\n",
    "import cv2\n",
    "import time\n",
    "\n",
    "import win32com.client as comctl\n",
    "wsh = comctl.Dispatch(\"WScript.Shell\")\n",
    "\n",
    "wsh.AppActivate(\"chromedino.com\")\n",
    "\n",
    "tree_x,tree_y,tree_w,tree_h=(140,50,50,80)\n",
    "\n",
    "while(True):\n",
    "\n",
    "    printscreen=np.array(ImageGrab.grab(bbox=(600,200,1300,350)))\n",
    "    printscreen=cv2.cvtColor(printscreen, cv2.COLOR_BGR2RGB)\n",
    "    \n",
    "######################## Detecting Trees ########################\n",
    "        \n",
    "    tree_window=printscreen[tree_y:tree_y+tree_h,tree_x:tree_x+tree_w]\n",
    "    \n",
    "    ret,tree_window_thresh=cv2.threshold(tree_window,127,255,cv2.THRESH_BINARY)\n",
    "    \n",
    "    tree_no_black = np.count_nonzero(tree_window_thresh==0)\n",
    "    tree_no_pixels = np.size(tree_window_thresh)\n",
    "    \n",
    "    tree_ratio=tree_no_black/tree_no_pixels\n",
    "\n",
    "    \n",
    "    cv2.rectangle(printscreen,(tree_x,tree_y,tree_w,tree_h),(0,0,255),2)\n",
    "\n",
    "    \n",
    "    if(tree_ratio>0.05):\n",
    "        \n",
    "        cv2.rectangle(printscreen,(tree_x,tree_y,tree_w,tree_h),(0,0,255),-1)\n",
    "        cv2.putText(printscreen,\"UP\",(tree_x,tree_y-10),cv2.FONT_HERSHEY_SIMPLEX,1,(0,0,255),2)\n",
    "        wsh.SendKeys(\"{UP}\")\n",
    "    \n",
    "        \n",
    "    cv2.imshow('printscreen',printscreen)\n",
    "\n",
    "    if cv2.waitKey(1)==27:\n",
    "        cv2.destroyAllWindows()\n",
    "        break\n",
    "    \n",
    "    keyPressed=0"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "application/javascript": [
       "$('#menubar').toggle();\n"
      ],
      "text/plain": [
       "<IPython.core.display.Javascript object>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "%%javascript\n",
    "$('#menubar').toggle();"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.8"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
