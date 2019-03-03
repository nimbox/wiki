Para colocar safari en resolución `1280 × 720` hay que ejecutar el
siguiente apple script:

    tell application "Safari"
        activate
        set the properties of front window to {bounds:{1, 1, 1280 + 1, 720 + 1}}
    end tell
