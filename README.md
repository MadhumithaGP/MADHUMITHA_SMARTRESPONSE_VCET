# MADHUMITHA_SMARTRESPONSE_VCET
import openai

# Set your OpenAI API key
openai.api_key = "your_openai_api_key"

def generate_response(client_input):
    """
    Generates a human-like email response using OpenAI's GPT API.

    Parameters:
        client_input (dict): A dictionary containing the client's details and project requirements.
    
    Returns:
        str: The generated email response.
    """
    # Construct the prompt
    prompt = f"""
You are a professional project manager drafting an email to a client. The email should sound polished, professional, and human-like. Avoid overly robotic phrases. Adapt naturally to the client's unique input and tone. 

Client Information:
- From Name: {client_input['from_name']}
- Client First Name: {client_input['client_first_name']}
- Client Last Name: {client_input['client_last_name']}
- Client Email: {client_input['client_email']}
- Client Country: {client_input['client_country']}
- Client Location: {client_input['client_location']}
- Client Language: {client_input['client_language']}
- Project Type: {client_input['project_type']}
- Service Category: {client_input['service_category']}
- Client Website: {client_input['client_website']}
- Additional Information: {client_input['additional_info']}

Compose an email that acknowledges the request, summarizes their requirements, and suggests the next steps while maintaining a professional tone.
"""

    # Call OpenAI's API
    response = openai.Completion.create(
        engine="text-davinci-003",
        prompt=prompt,
        max_tokens=300,
        temperature=0.7,
    )

    # Return the generated email response
    return response.choices[0].text.strip()


if __name__ == "__main__":
    # Example input
    client_input = {
        "from_name": "Jesna",
        "client_first_name": "Geminas",
        "client_last_name": "Ket",
        "client_email": "GeminasKet@gmail.com",
        "client_country": "Romania",
        "client_location": "Romania",
        "client_language": "English",
        "project_type": "Content with Databases",
        "service_category": "Web Development",
        "client_website": "No",
        "additional_info": """I need 4 dynamic pages for a real estate Web-application: one each for apartments, houses, business centres, and land. 
        I need 2 filters for 'for sale' and 'for rent,' and they should be connected. Don't bother with the design; I'll handle that. 
        I just need the functionality. The budget should be $100000. Thank you!"""
    }

    # Generate the response
    email_response = generate_response(client_input)
    print("Generated Email Response:\n")
    print(email_response)
