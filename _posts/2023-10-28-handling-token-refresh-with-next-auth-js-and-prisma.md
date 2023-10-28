---
layout: post
title: Handling Token Refresh with NextAuth.js and Prisma
type: post
published: true
excerpt: "Subsequent logins or signins have stale access tokens."
comments: true
tags: [prisma, next.js, nextauth]
---


NextAuth.js is a popular authentication library for Next.js applications. It makes it easy to set up authentication providers and handle user sessions. However, one challenge that developers often face is ensuring that OAuth tokens remain fresh. This article outlines how to handle token refresh with NextAuth.js and Prisma.

## Overview

When integrating OAuth providers like Google or Discord, it's essential to handle token refresh to ensure that the tokens remain valid. This is particularly important for scenarios where your application needs to make authenticated requests to third-party APIs on behalf of the user.

In this guide, we'll look at how to handle token refresh using the `signIn` and `signOut` events provided by NextAuth.js, and how to update the token information in the database using Prisma.

## Prerequisites

- A Next.js application with NextAuth.js and Prisma set up.
- OAuth set up with a provider like Google or Discord.

## Updating Tokens on Sign-In

When a user signs in, we can use the `signIn` event to update the token information in the database. This is where you add the code snippet for handling the sign-in event.

<code>

export const authOptions: NextAuthOptions = {
  callbacks: {
    // ...other callbacks
  },
  events: {
    signIn: async (message) => {
      console.log("signIn", JSON.stringify(message, null, 2));
      const { account, user } = message;
      const { access_token, refresh_token, expires_at } = account!;
      
      await prisma.account.updateMany({
        data: {
          access_token,
          refresh_token,
          expires_at,
        },
        where: {
          AND: [
            {
              userId: user.id,
              provider: "google",
            },
          ],
        },
      });
      console.log(`Added user account with ID: ${user.id}`);
    },
    // ...other events
  },
  // ...other options
};
</code>

## Clearing Tokens on Sign-Out

Similarly, when a user signs out, we may want to clear the token information from the database. This section will provide the code snippet for handling the sign-out event.

<code>
events: {
    // ...other events
    signOut: async (message) => {
      console.log("signOut", JSON.stringify(message, null, 2));
      const { userId } = message.session as unknown as { userId: string };
 
      try {
          await prisma.account.updateMany({
            data: {
              access_token: null,
              refresh_token: null,
              expires_at: null,
            },
            where: {
              AND: [
                {
                  userId: userId,
                  provider: "google",
                },
              ],
            },
            
          });
        
        console.log(`Deleted user account with ID: ${userId}`);
      } catch (error) {
        console.error(`Failed to delete user account with ID: ${userId}`, error);
      }
    },
},

</code>

## Conclusion

Handling token refresh is crucial for maintaining a smooth user experience and ensuring that your application can continue to interact with third-party services on the user's behalf. By leveraging the `signIn` and `signOut` events provided by NextAuth.js, and using Prisma to interact with your database, you can ensure that your OAuth tokens remain fresh and functional.

---
