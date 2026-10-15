---
kind: "company-prep"
title: "Interview Dry Run"
collection: "City of Oklahoma"
topic: "Interview Prep"
imported: "2026-10-13"
source_files: ["INTERVIEW PREP NOTES/City of oklahoma/Interview Dry Run.docx","INTERVIEW PREP NOTES/City of oklahoma/Interview Dry Run.pdf"]
tags: ["career/library"]
source_status: "source-claims-not-verified"
---

# Interview Dry Run

[[The Climb/Career Library/Career Library]]

> [!info] Source context
> Historical preparation or source notes. First-person stories and numeric outcomes remain source claims until confirmed; this import does not verify them.

**Dry Run: Software Engineer Interview**

**Interviewer**: Thank you for joining us, Neel. Let's start with you telling us a bit about yourself and your background.

**Neel**: Thank you for having me. My name is Neel Gali, and I recently completed my MS in Computer Science from Oklahoma State University. I have experience as a Full Stack Developer at Oklahoma State University and ZeMoSo Technologies, and as a Software Developer Intern at Monarch Tractor. I have a strong background in various programming languages and frameworks, including Python, Ruby, Java, JavaScript, C#, React, and Angular. I'm also well-versed in cloud platforms like AWS, GCP, and Azure. I enjoy working on challenging projects and am excited about the opportunity to contribute to the City of Oklahoma City's Software Development Program.

**Interviewer**: Great. Can you tell me about a project where you had to solve a complex problem? How did you approach it?

**Neel**: Certainly. While working at Oklahoma State University, we faced performance bottlenecks with our API endpoints, which slowed down the user experience. I took the initiative to refactor these APIs, consolidating multiple endpoints into fewer, more efficient ones. Additionally, I implemented lazy loading for image-heavy content, reducing initial page load times by 30%. By optimizing our database queries and adding indexes to frequently queried fields, we improved data retrieval speeds by 15%. These changes collectively enhanced the application's performance significantly.

**Interviewer**: That's impressive. How do you ensure your code is maintainable and follows best practices?

**Neel**: I adhere to coding standards and best practices by writing clean, modular, and well-documented code. I also conduct and participate in regular code reviews to ensure consistency and quality across the codebase. Additionally, I write unit tests to verify the functionality of my code and use continuous integration tools to automate testing and deployment processes. These practices help maintain code quality and make it easier for other team members to understand and work with the code.

**Interviewer**: Can you describe a time when you had to work closely with cross-functional teams? How did you handle communication and collaboration?

**Neel**: At ZeMoSo Technologies, I worked on a scientific experiment tracking platform that required close collaboration with the UI/UX team, backend developers, and project managers. We held daily stand-ups to discuss progress, challenges, and next steps. I made sure to communicate technical details in a way that non-technical team members could understand, ensuring everyone was on the same page. This collaborative approach helped us deliver a consistent and high-quality product.

**Interviewer**: How familiar are you with CI/CD pipelines and Azure DevOps?

**Neel**: I have extensive experience with CI/CD pipelines and Azure DevOps. For instance, during my internship at Monarch Tractor, I was responsible for setting up and maintaining CI/CD pipelines using Azure DevOps. I automated the build, test, and deployment processes to ensure continuous integration and delivery of our software applications. This not only improved the efficiency of our development workflow but also helped catch and resolve issues early in the development cycle.

**Interviewer**: We value continuous improvement. Can you give an example of how you've applied this in your work?

**Neel**: Continuous improvement is integral to my work philosophy. For example, at Oklahoma State University, I noticed that our deployment process had recurring issues that caused delays. I implemented logging and monitoring tools to detect and address potential issues promptly. This proactive approach reduced deployment-related issues significantly and improved the overall reliability of our application.

**Interviewer**: Excellent. Let's move on to a coding challenge. Please share your screen and open a notepad.

**Neel**: Sure, I'll do that now.

**Interviewer**: Here's a simple problem: Write a function in Python that takes an array of integers and returns the indices of the two numbers that add up to a specific target.

**Neel**: Okay, I'll start by defining the function and iterating through the array to check for pairs that sum up to the target.

python

Copy code

def two_sum(nums, target):

    seen = {}

    for i, num in enumerate(nums):

        complement = target - num

        if complement in seen:

            return [seen[complement], i]

        seen[num] = i

    return []

# Example usage:

print(two_sum([2, 7, 11, 15], 9))  # Output: [0, 1]

**Interviewer**: Can you explain your approach?

**Neel**: Sure. I used a dictionary to keep track of the numbers we have seen and their indices. As we iterate through the array, we calculate the complement of the current number with respect to the target. If the complement is already in the dictionary, it means we have found the pair that sums up to the target, and we return their indices. Otherwise, we add the current number and its index to the dictionary.

**Interviewer**: Great job. Your approach is efficient with a time complexity of O(n). Do you have any questions for us?

**Neel**: Yes, I would like to know more about the team I'll be working with and the types of projects I'll be involved in. Also, what are the key challenges the team is currently facing?

**Interviewer**: You'll be working with a diverse team of developers, project managers, and analysts. We are currently focusing on modernizing our existing applications and integrating new technologies to improve efficiency. One of the key challenges is ensuring seamless integration of new systems with our legacy infrastructure while maintaining high performance and reliability. We look forward to having someone with your skills and experience to help us tackle these challenges.

**Neel**: That sounds exciting. I'm looking forward to the opportunity. Thank you for your time.

**Interviewer**: Thank you, Neel. We appreciate your interest in the position and look forward to potentially working with you. Have a great day!

**Neel**: You too. Goodbye.

## Original documents in the vault

- [[The Climb/Career Library/_Attachments/Company Packs/Interview Dry Run-8baa2020.pdf|Interview Dry Run-8baa2020.pdf]]

![[The Climb/Career Library/_Attachments/Company Packs/Interview Dry Run-8baa2020.pdf#height=420]]

## Source provenance

- [Original DOCX](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/INTERVIEW%20PREP%20NOTES/City%20of%20oklahoma/Interview%20Dry%20Run.docx) · INTERVIEW PREP NOTES/City of oklahoma/Interview Dry Run.docx
- [Original PDF](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/INTERVIEW%20PREP%20NOTES/City%20of%20oklahoma/Interview%20Dry%20Run.pdf) · INTERVIEW PREP NOTES/City of oklahoma/Interview Dry Run.pdf

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
