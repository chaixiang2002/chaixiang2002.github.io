vendor/ntimespace/Space9dService/src/com/android/server/MessageHandler.java

```java
ClipboardManager cm = (ClipboardManager) mService.mContext.getSystemService(Context.CLIPBOARD_SERVICE);
cm.setPrimaryClip(ClipData.newPlainText("client", c_text));

if (paste) {
	boolean suc = commitText(c_text);
}

private boolean commitText(String text) {
    IInputContext input = mService.getInputContext();
            input.commitText(text, 1);
    return false;
}

```

frameworks/base/core/java/com/android/internal/view/IInputContext.aidl

frameworks/base/core/java/com/android/internal/view/IInputConnectionWrapper.java        extends IInputContext.Stub

```java
public void commitText(CharSequence text, int newCursorPosition) {
    dispatchMessage(obtainMessageIO(DO_COMMIT_TEXT, newCursorPosition, text));
}

Message obtainMessageIO(int what, int arg1, Object arg2) {
    return mH.obtainMessage(what, arg1, 0, arg2);
}

void dispatchMessage(Message msg) {
    // If we are calling this from the main thread, then we can call
    // right through.  Otherwise, we need to send the message to the
    // main thread.
    if (Looper.myLooper() == mMainLooper) {
        executeMessage(msg);
        msg.recycle();
        return;
    }

    mH.sendMessage(msg);
}
void executeMessage(Message msg) {
    case DO_COMMIT_TEXT: {
        Trace.traceBegin(Trace.TRACE_TAG_INPUT, "InputConnection#commitText");
        try {
            InputConnection ic = getInputConnection();
            if (ic == null || !isActive()) {
                Log.w(TAG, "commitText on inactive InputConnection");
                return;
            }
            ic.commitText((CharSequence) msg.obj, msg.arg1);
        } finally {
            Trace.traceEnd(Trace.TRACE_TAG_INPUT);
        }
        return;
    }
}
```

frameworks/base/core/java/android/view/inputmethod/InputConnection.java

```
boolean commitText(CharSequence text, int newCursorPosition);
```

frameworks/base/core/java/android/view/inputmethod/BaseInputConnection.java                           -implements InputConnection 

```java
public boolean commitText(CharSequence text, int newCursorPosition) {
    if (DEBUG) Log.v(TAG, "commitText " + text);
    replaceText(text, newCursorPosition, false);
    sendCurrentText();
    return true;
}

private void sendCurrentText() {
    if (!mFallbackMode) {
        return;
    }

    Editable content = getEditable();
    if (content != null) {
        final int N = content.length();
        if (N == 0) {
            return;
        }
        if (N == 1) {
            // If it's 1 character, we have a chance of being
            // able to generate normal key events...
            if (mKeyCharacterMap == null) {
                mKeyCharacterMap = KeyCharacterMap.load(KeyCharacterMap.VIRTUAL_KEYBOARD);
            }
            char[] chars = new char[1];
            content.getChars(0, 1, chars, 0);
            KeyEvent[] events = mKeyCharacterMap.getEvents(chars);
            if (events != null) {
                for (int i=0; i<events.length; i++) {
                    if (DEBUG) Log.v(TAG, "Sending: " + events[i]);
                    sendKeyEvent(events[i]);
                }
                content.clear();
                return;
            }
        }

        // Otherwise, revert to the special key event containing
        // the actual characters.
        KeyEvent event = new KeyEvent(SystemClock.uptimeMillis(),
                                      content.toString(), KeyCharacterMap.VIRTUAL_KEYBOARD, 0);
        sendKeyEvent(event);
        content.clear();
    }
}

private void replaceText(CharSequence text, int newCursorPosition,
                         boolean composing) {
    final Editable content = getEditable();
    if (content == null) {
        return;
    }

    beginBatchEdit();

    // delete composing text set previously.
    int a = getComposingSpanStart(content);
    int b = getComposingSpanEnd(content);

    if (DEBUG) Log.v(TAG, "Composing span: " + a + " to " + b);

    if (b < a) {
        int tmp = a;
        a = b;
        b = tmp;
    }

    if (a != -1 && b != -1) {
        removeComposingSpans(content);
    } else {
        a = Selection.getSelectionStart(content);
        b = Selection.getSelectionEnd(content);
        if (a < 0) a = 0;
        if (b < 0) b = 0;
        if (b < a) {
            int tmp = a;
            a = b;
            b = tmp;
        }
    }

    if (composing) {
        Spannable sp = null;
        if (!(text instanceof Spannable)) {
            sp = new SpannableStringBuilder(text);
            text = sp;
            ensureDefaultComposingSpans();
            if (mDefaultComposingSpans != null) {
                for (int i = 0; i < mDefaultComposingSpans.length; ++i) {
                    sp.setSpan(mDefaultComposingSpans[i], 0, sp.length(),
                               Spanned.SPAN_EXCLUSIVE_EXCLUSIVE | Spanned.SPAN_COMPOSING);
                }
            }
        } else {
            sp = (Spannable)text;
        }
        setComposingSpans(sp);
    }

    if (DEBUG) Log.v(TAG, "Replacing from " + a + " to " + b + " with \""
                     + text + "\", composing=" + composing
                     + ", type=" + text.getClass().getCanonicalName());

    if (DEBUG) {
        LogPrinter lp = new LogPrinter(Log.VERBOSE, TAG);
        lp.println("Current text:");
        TextUtils.dumpSpans(content, lp, "  ");
        lp.println("Composing text:");
        TextUtils.dumpSpans(text, lp, "  ");
    }

    // Position the cursor appropriately, so that after replacing the
    // desired range of text it will be located in the correct spot.
    // This allows us to deal with filters performing edits on the text
    // we are providing here.
    if (newCursorPosition > 0) {
        newCursorPosition += b - 1;
    } else {
        newCursorPosition += a;
    }
    if (newCursorPosition < 0) newCursorPosition = 0;
    if (newCursorPosition > content.length())
        newCursorPosition = content.length();
    Selection.setSelection(content, newCursorPosition);

    content.replace(a, b, text);

    if (DEBUG) {
        LogPrinter lp = new LogPrinter(Log.VERBOSE, TAG);
        lp.println("Final text:");
        TextUtils.dumpSpans(content, lp, "  ");
    }

    endBatchEdit();
}
```







---

input获取

```java
//vendor/ntimespace/Space9dService/src/com/android/server/Space9dManagerService.java
import com.android.internal.view.IInputContext;

private IInputContext mInputContext;

public IInputContext getInputContext() {
    return mInputContext;
}

@Override
public void syncInputContext(IInputContext inputContext) throws RemoteException {
    if (inputContext != null) {
        mInputContext = inputContext;
    }
}
```

