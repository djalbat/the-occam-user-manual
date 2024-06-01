## Unicode

The first of the points at the beginning of this chapter suggested that any grammar needs a collection of characters or symbols.
In Occam's case this is Unicode, a near ubiliquitous standard that encompasses close to 150,000 characters to date and has the potential to support over a million.
These characters are organised across various planes, namely the basic multilingual plane, or BNP for short, together with sixteen so-called astral planes.
For example, the aforementioned double-struck `ℕ` character, being regularly used in mathematical texts, can be found in the basic multilingual plane.
On the other hand the `𝔸` character, being far less common, is relegated to an astral plane.
In practice the position of a Unicode character, called its code point, is immaterial.
As mentioned in the previous chapter, the Occam IDE has a Unicode picker to enable you to pick from a large selection of Unicode characters without knowing their code points.

Brief mention should also go the JuliaMono typeface, [^juliamono] which is used in the editor and which has support for thousands of Unicode characters.

[^juliamono]: https://juliamono.netlify.app/
