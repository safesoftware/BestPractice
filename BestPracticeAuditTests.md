# Best Practice Reports #

## Report 1: HEADER ##

**Header 1: Title**

**Header 2: General Information**

- Warnings about the limit of this procedure. 
- Note current build number.
- Report name, generation datetime, workspace analyzed

---

## Report 2: WORKSPACE ##

**Workspace 1: Workspace Version**

- Test which version of FME the last edits were made in compared to the current FME version.
	- If last edits are an older version, WARN about testing before deploying on the current version.
	- If last edits are a newer version, FAIL. Give an ERROR about using a beta build to construct a workspace.
	- If last edits are the same version, PASS.

**Workspace 2: Workspace Properties**

- Test for name and category being set.
	- If one or the other are not set, WARN about this being bad for Best Practice.
	- If both are set, PASS.
 
---

## Report 3: STYLE ##

**Style 1: Bookmarks**

- Test for no bookmarks.
	- If there are no bookmarks, FAIL. Give an ERROR about this being bad for Best Practice.
- Calculate the number of transformers per bookmark.
	- If there are too few bookmarks (>10 transformers per bookmark), WARN as being bad for Best Practice
	- If there are too many bookmarks (<5 transformers per bookmark), WARN as being bad for Best Practice
	- If there are an appropriate number of bookmarks, PASS.
	
**Style 2: Annotations**

- Test for no annotations.
	- If there are no annotations, FAIL. Give an ERROR about this being bad for Best Practice.
- Calculate the number of transformers per annotation.
	- If there are too few annotations (>5 transformers per annotation), WARN as being bad for Best Practice
	- If there are too many annotations (<3 transformers per annotation), WARN as being bad for Best Practice
	- If there are an appropriate number of annotations, PASS.

---

## Report 4: BREAKPOINTS ##
 
**Breakpoints 1: Breakpoints**

- Check for breakpoints.
	- If there are enabled breakpoints, FAIL. Give an ERROR about putting a workspace into production with these.
	- If there are disabled breakpoints, WARN about putting a workspace into production with these.
	- If there are no breakpoints, PASS.

---

## Report 5: READERS ##

**Readers 0: Zero Readers**

- Check for no Readers at all.
	- If there are no readers, bypass other tests. Give a generic No Readers message.
	
**Readers 1: Build Number**

- Check each reader's "Generate Build" number against the current FME version.
	- If the Generate Build was an older version, WARN suggesting upgrade before deploying on the current version.
	- If there are no older versions, PASS.

**Readers 2a: Disabled Readers**

- Check for disabled readers.
	- If there are disabled readers, WARN that these are not useful when putting a workspace into production.
	- If there are no disabled readers, PASS.

**Readers 2b: Disabled Feature Types**

- Check for disabled feature types.
	- If there are disabled feature types, WARN that these are not useful when putting a workspace into production.
	- If there are no disabled feature types, PASS.
		
**Readers 3: Dangling Readers**

- Check for dangling readers (those without a feature type).
	- If there are dangling readers, FAIL. Give an ERROR that these are positively bad when putting a workspace into production.
	- If there are no dangling readers, PASS.
	
**Readers 4: Excess Feature Types**

- Check for a reader with >10 feature types.
	- If there are readers with >10 feature types, WARN that this indicates the possible need for a merge filter.
	- If there are no readers with >10 feature types, PASS.

**Readers 5: Published Parameters**

- Check for basic reader parameters still published.
	- If there are basic reader parameters still published, WARN that these might not be required.
	- If there are no basic reader parameters still published, PASS.

**Readers 6: Unconnected Feature Types**

- Check for reader feature types whose name is not a match in the connections list
	- If there are feature types without a match, WARN that these could affect performance and should be removed
	- If there are no unconnected feature types, PASS.

---

## Report 6: WRITERS ##

**Writers 0: Zero Writers**

- Check for no Writers at all.
	- If there are no writers, bypass other tests. Give a generic No Writers message.

**Writers 1: Build Number**

- Check each writer's "Generate Build" number against the current FME version.
	- If the Generate Build was an older version, WARN suggesting upgrade before deploying on the current version.
	- If there are no older versions, PASS.
		
**Writers 2a: Disabled Writers**

- Check for disabled writers.
	- If there are disabled writers, WARN that these are not useful when putting a workspace into production.
	- If there are no disabled writers, PASS.

**Writers 2b: Disabled Feature Types**

- Check for disabled feature types.
	- If there are disabled feature types, WARN that these are not useful when putting a workspace into production.
	- If there are no disabled feature types, PASS.
	
**Writers 3: Dangling Writers**

- Check for dangling writer (those without a feature type).
	- If there are dangling writers, WARN that these are not useful when putting a workspace into production.
	- If there are no dangling writers, PASS.
	
**Writers 4: Invalid Feature Type Names**

- Check for writer feature type names with possibly invalid characters
	- If there are characters outside of A-Z,a-z,0-9, WARN that these may be invalid (though FME should handle anyway).
	- If there are no characters outside of A-Z,a-z,0-9, PASS.

**Writers 5: Mixed Case Attr Names**

- Check Writer Attr Names for instances of mixed-case names (eg some UPPER, some lower, some MixedCase)
	- If there are mixed-case names, WARN that this is not good practice.
	- If there are no mixed-case names, PASS. 
	
**Writers 6: Coordinate Systems**

- Check for a writer setting a coordinate system.
- Check for a reader setting a coordinate system.
- Check for a CoordinateSystemSetter transformer.
	- If a writer sets a coordinate system, and no reader sets it, and there is no CoordinateSystemSetter, WARN that FME needs to know what to reproject from
	- If there are no writers with coordinate systems, or there are but a reader/transformer sets it, PASS.
		
**Writers 7: Published Parameters**

- Check for basic writer parameters still published.
	- If there are basic writer parameters still published, WARN that these might not be required.
	- If there are no basic writer parameters still published, PASS.

---

## Report 7: Transformers ##

**Transformers 1: Transformer Histogram**

- List the most-used transformers 

**Transformers 2: Percentage Check**

- Check percentage of overall count
	- If >25% are all the same type, WARN that this might not be a good scenario
	
**Transformers 3: Transformer Version**

- Check whether an update is required.
	- If a transformer is not the latest version, WARN
	
**Transformers 4: Inspectors and Loggers**

- Check for Inspector transformers
	- Enabled Inspectors = ERROR (note how bad this is for Server)
	- Disabled Inspectors = WARN
- Check for Logger transformers
	- Enabled Loggers = ERROR (note how bad this is for Server)
	- Disabled Loggers = WARNING

**Transformers 5: FMEFunctionCaller**

- Check for FMEFunctionCaller transformers
	- If one exists, it indicates low-level badness. WARN (but a very strong one)

**Transformers 6: Similar Parameters**

- Check for transformer parameters that are the same value
	- Suggest these might be better as a user parameter (possibly private) or Custom Transformer: WARN
 
---

## Report 8: PERFORMANCE ##

**Performance 0: Zero Transformers**

- Check for no transformers at all.
	- If there are no transformers, bypass other transformer-related tests. Give a generic No Transformers message.
		
**Performance 1: Parallel Processing**

- Check parallel processing parameters for use of Aggressive or Extreme.
	- If there are cases of Aggressive or Extreme, WARN that this may not guarantee good performance.
	- If there are no cases of Aggressive or Extreme, PASS.

**Performance 2: Parallel Processing 2**

- Check for multiple uses of Parallel Processing.
	- If there are multiple uses, WARN that this may spawn too many processes.
	- If there are not multiple uses, PASS.

**Performance 3: Performance Parameters**

- Check for use of transformers with parameters for performance improvements (eg Clippers first)
- Tests for Clipper/Displacer/FeatureMerger/NeighborFinder/PointOnAreaOverlayer/SpatialFilter
	- If such transformers exist, but don't use that parameter, WARN that this may impact performance.
	- If such transformers exist, and use that parameter, PASS.

---

## Report 9999: SUMMARY ##

**Summary 1**

- List the number of Errors
	
**Summary 2**

- List the number of Warnings

