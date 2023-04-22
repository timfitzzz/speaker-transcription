# Diarizing and Transcribing a NoPixel Server Day Using Pyannote and Whisper

Here's the flow:

1. Define times UTC for scheduled server restarts.
    - Have these times span Date ranges so that if there are exceptions you can just break the initial range and create a second instantiation, etc.
2. Scrape HasRoot for the streams that were live on that server at that time.
3. Now slide the conceptual playhead forward from the start of the time slot. At each increment:  

    a. Diarize each live stream, creating searchable embeddings for each of the speakers present in those streams.    

      1. Touch a Speaker record for each identified speaker, i.e. use the embedding to search and then either create one if there's no math or add this segment to the record 
      2. Touch Segment records for each of the transcribed segments.
      3. Create audit artifacts: four .mp4s to match four segments.


    a-sidequest. Determine where speakers overlap. Download these segments. Record them as PointsOfInterest, making sure to record the time ranges and people related. These may be the highest priority segments to reference when we're further ahead of them, if memory grows short.

    b. collect chat logs for each vocalization Segment  
      1. start from beginning of snippet to x seconds after it ends (10?)  
      2. Add to Segment

    c. collect still images of the start, middle, and end of each diarized Segment. these are gonna have to be pretty low-res, i think. good luck to you, me. use image2text to summarize image and save to Segment.
    
    d. transcribe each segment of dialogue, including within the prompt the segments constructed to match other speakers involved in the segment, if overlap was found

    e. use an LLM to summarize each segment based on the recorded dialogue and add that to the segment as well.

    f. move to the next segment, according to:
      - segments that overlapped with this segment's window but ran longer, starting from the point of overrun, proceeding in order of continuing duration
      - the next segment to start among all of those at this position
    
4. At this point, you should have:
  - A record of which speakers overlapped with each other and when
  - Points of Interest that can be highlighted for further use
  - A summary of what speakers said and any other detail that could be inferred from audio, chat, and snapshots for each bit of dialogue

Now, give all this to a good LLM and ask it to summarize what's happened, or pull clips from the points of interest, or simply talk about what happened from a single point of view. 

And then, I think for now, feed all of this into a content strategy, because that's the fastest way to use it to boost attention and interest in RP rather than to mechanize it and dry it out. Give LSBN the ability to break the fourth wall and cover it, or have somebody like Raine turn it into a daily show style digest. The sky's the limit.

That's it. That's the idea.