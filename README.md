# consoletest
A test utility for scripting stdin and stdout interactive console applications.

Tests are constructed by subclassing `ConsoleTest`. This allows you to use the
`assertConversation` function to check for correct interactive conversations.
```kotlin
import com.pcholt.console.testutils.ConsoleTest
import org.junit.Test

class AnimalJavaTest : ConsoleTest() {
    @Test
    fun `should have a simple conversation`() {
       assertConversation(
          """
            WHAT'S YOUR NAME? {PAUL}
            YOUR NAME IS PAUL? {YES}
            THANKS FOR PLAYING
            """
       ) {
          // The game's Main method
          main()
       }
    }
}
```

Curly brackets are the expected user input.
Note - this is actually just a way of defining the expected input as "PAUL" and "YES" 
and not that the input happens at the exact prompt position. Thus this is equivalent:
```kotlin
"""
{PAUL} {YES} WHAT'S YOUR NAME? 
YOUR NAME IS PAUL?
THANKS FOR PLAYING
"""
```

Amounts of whitespace are not counted, but whitespace is significant: You will get a failure if
your game emits `"NAME?"` when it expects `"NAME ?"`.
