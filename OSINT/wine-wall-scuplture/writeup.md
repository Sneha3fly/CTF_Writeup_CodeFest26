**The Wine & Wall Sculpture**

Category: OSINT

Difficulty: Medium

File Provided: Image of a wine holder

Objective: Identify the restaurant, sculpture designer, and artwork length

________________________________________
Approach

The task was to extract three pieces of information from a single image: the restaurant location, the sculpture’s designer, and its length.

I started with a reverse image search using Google Lens. This quickly pointed to a social media reference for @felukabeirut. Cross-checking images confirmed the location as Feluka Seafood Restaurant in Beirut, matching the sculpture shown in the challenge image.
Initially, I spent time browsing social media platforms (Instagram alternatives, Facebook/X pages, and comments) searching for technical details, but this did not yield useful information. I then pivoted from social media to architectural and technical sources.
A targeted search for:
*Feluka Seafood Restaurant wall sculpture*
led to a 3D Warehouse (SketchUp) model of the sculpture. The model page contained the key metadata (see attached image)
 
•	Designer: Waleed Abu Nassar
•	Length: 298.9
These details provided the remaining components needed to construct the flag.
________________________________________
Lessons Learned
•	Social media is effective for identification, but technical repositories often contain richer metadata.
•	When stuck, pivot from passive browsing to targeted keyword searches.
•	Architectural and 3D model repositories (e.g., 3D Warehouse, Sketchfab, TurboSquid) can be valuable OSINT sources.
•	Model descriptions frequently credit designers and include contextual information.
•	Embedded model properties can reveal precise measurements.
