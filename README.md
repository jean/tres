
# tres -- search Trello from the command line

## What is this? Why is this?

[Trello](http://www.trello.com) is one of these tools where you ask yourself how you could ever work without it, if you know it.
I use it at work, for my private projects and generally regard its combination of usability, ease of use and great API one
of the best packages you discover to better organize yourself and your team.

While there are many great add-ons, nearly all of them are integrated with the Trello GUI oder have been developed as web applications.
I, however, am an avid command line user and do a *lot* of scripting with bash, awk, Python and more recently Golang. So I decided
that I need a good command line tool to search thru all my Trello boards. Follwing the tradition of _"do one thing and do it well"_
I did not try to leverage to complete Trello API but focused on searching for cards and retrieving information.

Now it is a breeze to pipe Trello search results to your shell scripts or help your "stuck-in-the-spreadsheet-era" colleagues
to convert a list of several dozen Trello cards to their beloved Excel sheet. :-)


### Quick-Start

You need a CSV file of all Trello cards in your board "Recruiting" that have a label "PhoneInterview" assigned. You co-worker
asked you to provide the name, the date of the last activity and a link to the card.

    ./tres --format csv --fields "name,datelastactivity,shorturl"  search 'board:"Welcome Board" #Green'

That was easy! Here's the output (note that the links have been changed to point to nothing)

    Rosie Recruit    2015-08-14T15:36:33.249Z    https://trello.com/c/LinkLink
    Sheryl Sample    2015-08-04T08:42:12.001Z    https://trello.com/c/NotValid
    Harold Hire      2015-08-09T11:31:53.654Z    https://trello.com/c/12345678

As you see from the options that

 * we requested CSV format output (default is TAB-separated, LF as row delimiter)
 * we specified the fields that we needed for each card

The command `search`, followed by the search term tells the `tres` tool what to search for.
Search syntax is exactly what you would enter in the Trello search edit field in the browser.

### Usage Message

Executing `tres` without parameters or with `--help` displays the help screen below.


    Usage: tres [options] [command]

    Commands:
        search              'trello_search_query' | <filename>
                            see http://help.trello.com/article/808-searching-for-cards-all-boards
                            literal search query must be enclosed in single quotes
                            filename must contain a literal query without single quotes
        members "<name>"    retrieve members of the specified board
        boards              retrieve board name/id and and list name/id for each board

    Options:
        --colsep <string>   set column separator for result columns
        --rowsep <string>   set row separator for result lines
        --fields <string>   a comma-separated list of result field names for a search
        --format <string>   specify output format (one of: text|excel|csv|json|markdown)
        --limit <n>         limit number of resulting cards (default 200)

    List of field names:
        attachmentcount     hasdesc             labelcolors
        boardname           id                  labels
        checked             idattachmentcover   listname
        closed              idboard             name
        commentcount        idchecklists        pos
        comments            idlabels            shortlink
        datelastactivity    idlist              shorturl
        desc                idmembers           subscribed
        due                 idmembersvoted      url
        email               idshort

    Environment vars used:
        TRELLO_KEY          your Trello API key
        TRELLO_TOKEN        your Trello API token
        TRELLO_USER         optional (defaults to "me"), you Trello API user name

    If anything goes wrong, the tool exits with a return code of 1.


## Detailed Documentation

You can find more detailed documentation in the markdown file `reference.md` in this repo.

## Just give me the binary!

If you do not want to compile `tres` yourself or are in a hurry,
I provide compiled version for Mac OS X (darwin/amd64) and Windows (windows/386 and (windows/amd64) on my home page.
Here are the links:

 * Mac OS X [Download](http://www.arminhanisch.de/downloads/tres/macosx.zip)<br>
   MD5 hash: 7b6b04df1670ed3eea4fb2356274f15c
 * Windows 386 [Download](http://www.arminhanisch.de/downloads/tres/win32.zip)<br>
   MD5 hash: 43a921a17acd2527c1e0637fe8ff0a8b
 * Windows amd64 [Download](http://www.arminhanisch.de/downloads/tres/win64.zip)<br>
   MD5 hash: cc48e97d63b7162609a961360d144368

Please note: I work on a Mac, the builds above have been cross-compiled using Go 1.4.2,
USAGE OF THESE BINARIES IS AT YOUR OWN RISK, THE SOFTWARE IS PROVIDED "AS IS",
WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO
THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES
OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

