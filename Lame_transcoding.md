## Lame 库PCM转成mp3函数

```
public byte[] getMp3(byte[] pcm){
        byte[] _mp3OutputBuf = new byte[1024 * 10];
        int mp3BufLen = Lame.encode(pcm, pcm, pcm.length / 2, _mp3OutputBuf, _mp3OutputBuf.length);
        if(mp3BufLen < 0){
            LogBuffer.ONE.e(TAG, "mp3 encoder error:" + mp3BufLen);
            return null;
        }
        byte[] ret = new byte[mp3BufLen];
        System.arraycopy(_mp3OutputBuf, 0, ret, 0, mp3BufLen);
        Log.e(TAG, "mp3 length:" + ret.length);
        return ret;
    }

```
调用之前调用Lame.initializeEncoder(16000, 1)初始化一下
