Project Setup:

see original "README.md" file for the instruction. 

For the submission, I would like to point out: 

the project link, https://conferenceapp-0201.appspot.com/
all the newly added endpoints are working and checked in api explorer https://conferenceapp-0201.appspot.com/_ah/api/explorer. The newly added endpoints are 

Task 1: 

	- getConferenceSessions(websafeConferenceKey) -- Given a conference, return all sessions
	- getConferenceSessionsByType(websafeConferenceKey, typeOfSession) Given a conference, return all sessions of a specified type (eg lecture, keynote, workshop)
	- getSessionsBySpeaker(speaker) -- Given a speaker, return all sessions given by this particular speaker, across all conferences
	- createSession(SessionForm, websafeConferenceKey) -- open only to the organizer of the conference

To make it work, Session class model are added (including SessionForm). 
1. We understand each session only host one speaker, so speaker is naturally a attribute of Session class. 
2. Date: DateProperty, StartTime: TimeProperty (for query (in task 3)
3. Session is a child a conference

Task 2:

Similarly as the conferenceToAttend, the session wish list is implemented as memember of the profile class.

all three new endpoints are working 

	- addSessionToWishlist(SessionKey) -- adds the session to the user's list of sessions they are interested in attending
	- getSessionsInWishlist() -- query for all the sessions in a conference that the user is interested in
	- deleteSessionInWishlist(SessionKey) -- removes the session from the user¡¯s list of sessions they are interested in attending

Task 3: 

   a. Two new queries are implemented
      a.1. getSessionsByDate:          get all sessions, given a specific date, cross all conferences
	  a.2  getMorningSessionsByDate    get all sessions in the morning, given a specific date, crosses all conferences
  
   b. getNonWorkshopSessionsBeforeSevenPM
      This is implmented by endpoint getNonWorkshopSessionsBeforeSevenPM. 
	  Initially, this would be done by querying the starTime < 19:00 and typeOfSession != "workshop", however, the problem is that google app engine complaining "(Cannot have inequality filters on multiple properties")
	  so idea is that to bin one dimension, and cumulate, in this particular project, since the typeOfSession, only takes "lecture", "workshop", "keynote", so we enumerate in this dimension. The result looks good. 
	  
Task 4. 

This is done by combing both mecache key and task queue, the endpoint getFeaturedSpeaker works well. MEMCACHE_FEATURESPEAKER_KEY = "FEATURED_SPEAKER"