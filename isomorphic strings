bool isIsomorphic(char * s, char * t) {
    int mapS[256] = {0};
    int mapT[256] = {0};
    
    for (int i = 0; s[i] != '\0'; i++) {
        if ((mapS[(unsigned char)s[i]] && !mapT[(unsigned char)t[i]]) ||
            (!mapS[(unsigned char)s[i]] && mapT[(unsigned char)t[i]])) {
            return false;
        }
        if (!mapS[(unsigned char)s[i]] && !mapT[(unsigned char)t[i]]) {
            mapS[(unsigned char)s[i]] = i + 1;
            mapT[(unsigned char)t[i]] = i + 1;
        } else {
            if (mapS[(unsigned char)s[i]] != mapT[(unsigned char)t[i]]) {
                return false;
            }
            mapS[(unsigned char)s[i]] = i + 1;
            mapT[(unsigned char)t[i]] = i + 1;
        }
    }
    return true;
}
