I can not talk about my own play in Cryptography do to living in the United States and there being a chance that this will be read in other countries, because the United States has some messed up laws about export of Cryptographic algorithms (if it is developed in the United States it must be explicitly approved for export).

I will however speak about what I feel makes for good encryption.

# Good Encryption:

Good encryption should meet a few simple rules:
* The Algorithm(s) should be simple enough for any Computer User that codes at all to memorize.
* The encrypted data should 100% indistinguishable from true random data.
* There should be nothing about the encrypted data that can give away the plaintext (what we call non-encrypted data) in any way.
* There should not be any way to reverse the plaintext from the encrypted data.
* The byte order of the encrypted data should not match that of the plaintext.
* There should not be any way to derive the byte order without knowing the key.
* There should be no information about the key in the cryptotext.
* In its plaintext form the data encrypted should have some form of message validation.


While these may seem a bit obvious on the surface, there unfortunately are not any widely published encryption algorithms that meet all these requirements.  Some come close, though none meet all these points 100%.  Unfortunately the public key private key algorithms are the worse about meeting these requirements.

I have been developing my own encryption algorithms, and working with some good cryptographers to validate them.  I intend to continue to refine my personal understanding of this area of study until I am able to produce at least 4 different cryptographic algorithms that meet all of these requirements.  As cryptography is very important in our world of information, if for no reason other than to have some privacy, I am very hopeful that one day I will be able to share what I come up with (once I manage to meet all the requirements without exception).

It is also a huge hope that others that have an understanding of cryptography will be creating more algorithms that meet these rules.  The more that is around and shared as much as possible, the more that we can argue against restrictions on cryptography.


---
## Then we may need Steganography:

There may be a future where forces attempt to prevent the use of cryptography, in which case we will have to hide our encrypted data (cryptotext) in a way to prevent detection.  This is the art of steganography, and one that should be studied.

The ideals for steganography are:
* The embedded message must not be detectable by any means to anyone that does not know it is there.
* Whatever the message is hidden in must be able to be easily and widely distributed.
* For those that know of the message, the message must accurately contain the cryptotext being delivered.

Fairly simple rules.  Though care must be taken in the choices made.

For Example: If you embed it in a noisy lossless digital photograph or other picture file, there must not be any way to detect the data.  This means that the added noise of the message must be believable to someone that can analyze the picture file, the original must no longer exist anywhere on earth (as a comparison would show the differences), etc.

Similar issues for encoding in any media, digital or otherwise.  Care has to be taken to prevent the ability of the cryptotext to be detectable as existing at all in good steganography.  It is possible to use the plaintext, though this does not provide the same usefulness as using a strongly encrypted cryptotext of the data being transmitted.  Using cryptotext has the advantage also of already looking like random noise, and thus being reasonable to embed in something that has a level of true random nature.

Things need not be encoded with widely used means of stegonography, the only thing that matters is that both the message creator and the intended recipient both know how it is encoded.

In a picture, it could be the low value bit method, or it could be the absolute positions of certain depicted objects in the image, or there relative positions, or the relative angles between objects, the differences of relative angles, etc, etc.  There are many possible ways to hide information, be creative.

In a sound file the difference in pitch could be used, or the low bits of amplitude in white noise, or the exact timing of a particular reoccurring sound or instrument used.  It could even be a combination of multiple of the above.  Again there are many possibilities be creative.

In an animation or movie it could be any of the methods that apply to still pictures, and if the animation / movie has sound it could also be any of the methods that apply to sound.  Then it could also be the rate of change in movement, or the rate of change of acceleration of a movement through multiple frames, or the angle of movement, or the difference in angle of movement, or the difference between the angle of change of multiple objects, or the difference of the rate of change of the rate of change between multiple objects, or any combination of these bits of data.

If using multiple methods for the data, the method of recombining the data once extracted may help in how it is obscured.

Be creative, figure out better ways to keep your cryptotext from being able to be discovered.


---
## Why Here?

The reason for putting this note in a Wiki about YASDOE is that any Operating System development should also include thought of what will run on that Operating System.  In the modern world to maintain privacy any personal computer should have good means of encrypting data for transition in some way, and thus this must be thought about as something that will run on an OS being developed by any person or group.

That said encryption should have very little effect on the OS itself, as this is a higher level application than an OS.  Indeed any applications related to cryptography should be easily removed without have any effect on the operation of the system, in case of some force attempting to eliminate and/or limit the use of cryptography.


---
## Privacy is Important:

Many government agencies are already trying to argue that they should be able to decrypt some data without knowing the key / password.  People forget that just because it is government does not mean there is no corruption.  We have seen members of agencies of our governments abuse there power for personal reasons, or as favors to friends, it is more common place than many wish to admit.  Strong cryptography is already widely known, there is no way take it back and it is needed to maintain privacy in our personal interactions, as well as of our personal property including intellectual property.  Every single case that has been used to argue for allowing access is one where the data did not help over the other intelligence gathered without the data in question.

As an example, even though it is on a computer that is never connected to the internet or any network, I am writing a couple of novels (not all my work is incoherent like this) that I do not yet have proof of copyright for.  So just in case someone else looks at that computer I keep them encrypted using known unbreakable strong encryption, and then they are stored in a manner that takes advantage of strong steganography.  I do this so that I can maintain my Intellectual Property that may have future economic value to me.

There is also the thought, if you are in a courtship (dating) do you really want some stranger reading your correspondence, or listening in on your phone calls with each other?  Or if you are corresponding with your physician about a health problem, do you want to forfeit your privacy (do you know the reason for HIPPA)?  If we allow the any person, organization, government, or other group to have the ability to break our encrypted information we would be saying good bye to protecting our IP, good by to our health care privacy, good bye to our courtship privacy, etc.

There is also the detail of your personal financial information, when you make a purchase online.  Do you want random people to be able to access your bank account or credit card because you decided to make an online purchase?  Do you want people to take your money without your permission?  I think that we all want to keep this information as private as humanly possible, this requires encryption on the internet.

---
## A Very Bad Sign:

Today (June 17th, 2022ad)I learned that there is a bill in the United States congress that intends to restrict the use of strong encryption.  This bill attempts to outlaw any encryption for which law enforcement can not break without knowing the password or other key.  This would be a very bad sign.

This is hand in hand with an international group working towards a similar goal.

Both of these claim to be trying to prevent using the internet for criminal activity.  This can NOT work ever.  The issue is that if they do this they are effectively removing the ability for us to maintain needed privacy, and asking us to forfeit our money in total unless it is in physical cash form.

These measures can not be allowed to move forward, they are a hazard to our welfare on a global scale.  Those involved may not realize the repercussions of what they are proposing, this is not an excuse.  We must fight for our right to privacy.



---
BLAH
