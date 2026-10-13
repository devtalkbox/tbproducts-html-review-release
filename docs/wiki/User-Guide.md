# HTML Review User Guide

**Updated 13 October 2026 · Version 1.0.1**

Use the **admin console** to manage reviewer access and follow up on feedback. Use the **Electron desktop app** to browse a website, select an element, and post a comment with a screenshot. Both connect to the same review server, so saved threads and replies are shared.

Screenshots below show an isolated local demo with sample data. Desktop overview images combine captures of the app's website and comments views at their displayed positions. The `127.0.0.1` addresses are demo addresses; use your team's server and website URLs for everyday work.

## Console and download URLs

| Resource | URL |
| --- | --- |
| Admin console | [https://html-review-206149277907.asia-east1.run.app/](https://html-review-206149277907.asia-east1.run.app/) |
| Electron desktop app — macOS Apple silicon, v1.0.1 DMG | [https://github.com/devtalkbox/tbproducts-html-review-release/releases/download/v1.0.1/HTML.Review-1.0.1-arm64.dmg](https://github.com/devtalkbox/tbproducts-html-review-release/releases/download/v1.0.1/HTML.Review-1.0.1-arm64.dmg) |
| Latest release and available downloads | [https://github.com/devtalkbox/tbproducts-html-review-release/releases/latest](https://github.com/devtalkbox/tbproducts-html-review-release/releases/latest) |

Downloads are public; no GitHub account is required. The listed DMG is for Macs with Apple silicon (M series). Intel Mac, Windows and Linux downloads are available in the latest release.

## Before you begin

| What you need | Admin console | Electron app |
| --- | --- | --- |
| Review server | Your team's review server URL | The same review server URL |
| Sign in details | Admin username and password | Your display name and a reviewer access code |
| Website access | Admins can view all shared review threads | Your code must allow the website hostname |

The deployed console is at [HTML Review](https://html-review-206149277907.asia-east1.run.app/). Ask your administrator for credentials or an access code. Your display name appears on your comments and replies.

**Typical workflow:** an admin creates a code → a reviewer opens a website and posts feedback → the team replies → a resolved thread is archived.

## Use the admin console

### 1. Sign in

1. Open the review server URL in your browser.
2. Enter your **Username** and **Password**.
3. Click **Log in**. The console opens the **Reviews** section.

![Admin console login with username and password fields](images/console-login.png)

Admin credentials are separate from reviewer access codes. Use **Log out** in the top right when finished.

### 2. Create a reviewer access code

1. Select **Access codes**.
2. Enter a **Code label**, such as `Website review team`.
3. Under **Allowed hostnames**, enter each hostname and press **Enter**, or separate hostnames with commas.
4. Click **Create code** to generate a six digit code.
5. Click **Show code**, share the code privately with reviewers, then use **Hide code**. **Dismiss** closes the new code panel; the code remains under **Existing codes**.

![Access codes section showing the creation form, hostname chips, and hidden code values](images/console-access-codes.png)

Enter hostnames without a scheme, port, or path:

| Rule | Allows |
| --- | --- |
| `example.com` | Only `example.com` |
| `*.example.com` | Subdomains such as `www.example.com` and `staging.example.com`; excludes `example.com` itself |
| `example.com, *.example.com` | The main hostname and its subdomains |

Rules ignore ports. Add any hostname a website redirects to, including a separate sign in hostname when needed.

For an existing code:

- Edit its label or hostname chips, then click **Save changes**. Click a chip's **×** to remove a hostname.
- Use **Show code** and **Hide code** to reveal or conceal its value.
- **Revoke code** removes access for reviewers using that code, including existing sessions.
- **Resume code** makes a revoked code usable again.
- **Delete code** is available for revoked codes and permanently removes the code after confirmation.

For an older code that asks for its original value, enter that value once and click **Show code** to restore Show / Hide. If nobody knows the original, create a replacement code.

### 3. Find and read feedback

1. Select **Reviews**.
2. Choose a **Hostname**, or leave **All hostnames** selected.
3. Choose **Active**, **Archived**, or **All** under **Status**.
4. Choose **Newest first**, **Oldest first**, or **Recent activity** under **Sort**.
5. Select a row in the thread table to open its details on the right.

![Reviews section with filters, a thread table, and the selected thread screenshot](images/console-review-thread.png)

Each thread includes its number, comment, author, website URL, screenshot, selected element details, and replies. Use **Refresh** for new feedback and **Previous** / **Next** to move through result pages.

### 4. Reply and archive

1. Open an active thread.
2. Scroll through the details to the **Reply** field.
3. Write your response and click the send arrow, labeled **Post reply**.
4. When the issue is resolved, click **Archive thread**.

Archived threads remain available under **Status → Archived** or **All**. Select an archived thread and click **Unarchive thread** to reopen it. Replies are disabled while a thread is archived.

## Use the Electron desktop app

### 1. Launch the app

Download the package for your operating system from the [latest public release](https://github.com/devtalkbox/tbproducts-html-review-release/releases/latest).

| Platform | Launch |
| --- | --- |
| macOS Apple silicon or Intel | Open the matching DMG, drag **HTML Review** into **Applications**, then open it. |
| Windows x64 portable | Double-click `HTML.Review.Portable.1.0.1-x64.exe`. No installation is needed; runtime files extract to a temporary folder. |
| Windows x64 installer | Run `HTML.Review.Setup.1.0.1-x64.exe`, then open **HTML Review**. |
| Linux x64 | Make the AppImage executable and run it, as shown below. |

```sh
chmod +x HTML.Review-1.0.1-x64.AppImage
./HTML.Review-1.0.1-x64.AppImage
```

Version 1.0.1 connects to [the hosted review server](https://html-review-206149277907.asia-east1.run.app/) by default. You do not need Node.js, npm, or a command-line server argument. Ask your administrator for a reviewer access code. The app and admin console must use the same server.

macOS packages are ad-hoc signed and not notarized; Windows packages have no publisher certificate. Your operating system may show a security prompt. Windows and Linux builds have not been tested on their native operating systems.

To use another server, pass `--server` when launching the app, or set `REVIEW_SERVER_URL`. For an installed macOS app:

```sh
open -a "HTML Review" --args --server https://YOUR_REVIEW_SERVER
```

For the Windows portable app in PowerShell:

```powershell
.\HTML.Review.Portable.1.0.1-x64.exe --server https://YOUR_REVIEW_SERVER
```

The server URL must be an HTTPS origin, or an HTTP loopback origin for local development, without credentials, a path, query, or fragment. See the [download and setup README](../../README.md) for packages and checksums.

### 2. Sign in as a reviewer

1. Enter **Your name**. Choose a name teammates will recognize.
2. Enter the access code supplied by your administrator in **Auth code**.
3. Click **Sign in**.

![Electron app reviewer login with name, auth code, and Sign in controls](images/electron-login.png)

The app remembers your reviewer session across restarts. Sessions expire after 24 hours; sign in again when prompted. Website login is separate: sign in to the reviewed website inside the app if it requires an account.

### 3. Open a website

1. Enter the full website URL in the address bar, for example `https://staging.example.com`.
2. Click the arrow at the end of the address bar, labeled **Open page**.
3. Wait for the page to load. The website appears on the left and comments on the right.

![Electron workspace showing a website on the left and review controls on the right](images/electron-workspace.png)

The desktop app opens websites directly; they do not need an installed review script or permission to appear in an iframe.

Hover over icon buttons to see their names:

| Location | Control | Use |
| --- | --- | --- |
| Address bar | Previous page / Next page | Move through pages opened in the app |
| Address bar | Refresh page | Reload the website |
| Address bar | History | Reopen a previously visited URL |
| Address bar | Hide comments / Show comments | Toggle the comments panel |
| Address bar | Sign out | End the reviewer session |
| Comments toolbar | Pointer — Start selecting | Choose a website element to comment on |
| Comments toolbar | Speech bubble — Highlight commented elements | Show elements with active comments on this page |
| Comments toolbar | Download arrow — Export | Download an HTML report |
| Comments toolbar | Circular arrow — Refresh | Reload the comment list |

Drag the divider between the website and comments to resize the panels.

### 4. Select an element and write feedback

1. Click **Start selecting** in the comments toolbar.
2. Hover over the website to highlight elements.
3. Click the element you want to discuss.
4. The app captures the visible webpage and opens **Comment on this element** in the right panel.
5. Enter a clear description in **Your comment**, such as “Please shorten this headline to make the main message easier to scan.”

![Selected headline, captured screenshot, and comment draft in the Electron app](images/electron-new-comment.png)

Click **Stop selecting** or press **Escape** to return to normal browsing. Use the draft's **×**, labeled **Cancel comment**, to cancel a comment; confirm discarding it if you have unsaved changes.

### 5. Annotate the screenshot and save

1. Before posting, click the pencil on the screenshot, labeled **Edit screenshot**.
2. Choose **Brush** or **Rectangle**, a drawing color, and a line width.
3. Drag on the screenshot to draw. Use **Undo** or **Redo** to adjust your marks.
4. Click the disk icon, labeled **Save screenshot**, to apply the edits. The editor's **×**, labeled **Cancel**, closes it without applying new edits.
5. Back in the comment panel, click the send arrow, labeled **Save comment**.
6. Wait for **Comment saved** and the saved thread to appear.

![Screenshot editor with brush and rectangle tools, color, line widths, undo, redo, and save](images/electron-screenshot-editor.png)

**Screenshots are fixed after posting**, including for admins. Check the capture and annotations before saving. Capture covers the visible viewport and main document; nested iframes and shadow roots are excluded from element selection. Some cross origin images, video, or CSS may appear differently in the capture.

If a save fails, keep the draft open and retry **Save comment**. If the page changes and the draft becomes stale, cancel it and select the element again.

### 6. Read threads and reply

1. Use **Hostname**, **Show**, and **Sort** to filter the comment list.
2. Select a thread to view its screenshot, element details, and conversation.
3. Scroll to **Reply**, write your response, and click **Post reply**.
4. Use the top right **×**, labeled **Back to comments**, to return to the list.

![Saved Electron thread with its screenshot and the highlighted website element](images/electron-thread.png)

![Electron thread scrolled to the conversation and Reply field](images/electron-reply.png)

Click **Highlight commented elements** to mark elements with active threads on the current page. Right click a highlighted element to open its thread. A thread may be unmatched if the website's structure has changed since it was created.

### 7. Archive or reopen a thread

1. Open the thread.
2. Click **⋯**, labeled **Comment actions**, at the top right of the details panel.
3. Select **Archive thread** when the feedback is resolved.

![Electron Comment actions menu showing Archive thread](images/electron-thread-actions.png)

To reopen it, set **Show** to **Archived** or **All**, select the thread, and choose **Comment actions → Unarchive thread**. Archiving keeps its screenshot and conversation, and stops new replies until the thread is reopened.

### 8. Export an HTML report

1. Set the **Hostname**, **Show**, and **Sort** filters to the feedback you want to include.
2. Click **Export**, the download arrow in the comments toolbar.
3. Wait while screenshots are prepared and the app reports the exported comment count.
4. Open the downloaded `html-review-YYYY-MM-DD.html` file in a browser.

Export includes all matching result pages, along with screenshots and replies. To include resolved feedback, select **Show → All** before exporting. Reports contain review content and screenshots; share them only with the intended recipients.

## Troubleshooting

| Problem | What to do |
| --- | --- |
| Cannot sign in to the console | Check the server URL and admin username/password with your administrator. Reviewer codes do not work for admin login. |
| Reviewer code is rejected | Confirm the code and server URL with the administrator. The code may have been revoked. |
| Hostname is not authorized | Ask an admin to add the exact hostname, including any redirect or login hostname, to your code. Reopen the page after the change. |
| Start selecting is disabled | Wait for the website to load. Check the status message, then use Open page to retry. |
| Capture fails | Use Retry capture or select another element. |
| A draft says the page changed | Cancel the stale draft and select the element again on the current page. |
| Comment or reply fails to save | Keep the draft open, check your connection, and retry. |
| Cannot find a thread | Check Hostname and Active / Archived / All filters, then refresh. |
| Cannot reply | Check whether the thread is archived. Unarchive it to resume discussion. |
| App asks you to sign in again | Your session may have expired or your code may have been revoked. Sign in again or ask your administrator. |
| Website view disconnects or crashes | Click Open page to reload and reconnect the website. |
