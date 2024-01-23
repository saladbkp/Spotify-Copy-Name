# Spotify Tool

## Copy Name 

```c++
//Spotify class name
HWND handle = FindWindow(L"Chrome_WidgetWin_0", nullptr);

//GetWindowText function
wstring GetWndText(HWND hWnd)
{
    LRESULT length = SendMessageW(hWnd, WM_GETTEXTLENGTH, 0, 0);
    wchar_t* buf = new wchar_t[length + 1];
    SendMessageW(hWnd, WM_GETTEXT, (WPARAM)length + 1, (LPARAM)buf);
    wstring title = buf;
    delete[] buf;
    return title;
}

//Ctrl + V -> pass title
void CopyToClipboard(const wstring& text)
{
    if (OpenClipboard(nullptr))
    {
        EmptyClipboard();

        HGLOBAL hMem = GlobalAlloc(GMEM_MOVEABLE, (text.length() + 1) * sizeof(wchar_t));
        if (hMem)
        {
            wchar_t* pMem = static_cast<wchar_t*>(GlobalLock(hMem));
            if (pMem)
            {
                wcscpy_s(pMem, text.length() + 1, text.c_str());
                GlobalUnlock(hMem);
                SetClipboardData(CF_UNICODETEXT, hMem);
            }
        }

        CloseClipboard();
    }
}
```

## Issue In Process

- String in c++ use lib 

  #include <iostream>
  #include <string>
  #include <Windows.h>

  using namespace std;

- Japanese Chinese Korean -> Ansi 

  cannot use char or string 

  must use wstring (wide string)  

- import DLL 

## Usage

![usage](usage.gif)

1. Open Spotify 
2. Play a song
3. Run SpotifyTool.exe
4. Find a box Ctrl + V 

## lyricstify
run spotly.bat for lyrics + romanji
Any update refer this https://github.com/lyricstify/lyricstify