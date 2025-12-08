 
**Lesson 4: Unlocking AI Superpowers – How to Access Amazon Bedrock Models**

### The Gatekeeper Story  
Think of Amazon Bedrock like a massive arcade with 50+ game machines (AI models). Most doors are unlocked by default, but some premium games need a quick "Are you cool with the rules?" tap. This lesson shows you how to flip switches in the console to access any model – no coding needed. Once unlocked for your account, everyone in your team can play!

### Quick Access: Most Models Ready to Go  
Good news – **access is automatic** in commercial AWS regions if you have basic AWS Marketplace permissions. Just:  
- Open Bedrock console → **Model access** (left menu)  
- Click **Modify model access** → Check boxes for models you want  
- Hit **Submit** after reviewing EULA (terms of service)  

**Anthropic special step:** First-time? Fill a quick "What's your use case?" form – approved instantly![1]

### Step-by-Step Console Unlock  
```
1. Console → Bedrock → "Model access" under Configurations  
2. "Modify model access" → Select providers (Cohere, Meta, etc.)  
3. Group by provider → Check/uncheck all at once  
4. Anthropic? → "Submit use case details" form  
5. Review terms → "Submit" (takes 2-5 mins)  
```
Status changes to **"Access granted"** – done! Revoke anytime by unchecking.[1]

### IAM Power Moves for Teams  
**Block specific models:** Attach this policy to users/roles:  
```json
{
  "Effect": "Deny",
  "Action": "aws-marketplace:Subscribe",
  "Resource": "*",
  "Condition": {"aws-marketplace:ProductId": ["prod-m5ilt4siql27k"]}
}
```
**Stop usage after access:** Deny Bedrock actions on model ARN:  
```json
{
  "Effect": "Deny",
  "Action": "bedrock:*",
  "Resource": "arn:aws:bedrock:*::foundation-model/anthropic.claude-3-5-sonnet-20240620-v1:0"
}
```
Amazon/DeepSeek models? No Marketplace – just deny by model ID.[1]

### GovCloud & Pro Tips  
- **GovCloud users:** Link standard AWS ID → Access via us-east-1/us-west-2 → Use in GovCloud region  
- **Organizations:** Use SCPs to review EULAs centrally before enabling  
- **Agreeing = EULA accept** for 3rd-party models (one-time per account)  

Now your arcade is stocked – jump back to playgrounds and test all models!(see the generated image above)[2]

**Next?** Agents, RAG, or customization lesson? Share context!

[1](https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html)
[2](https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started-console.html)
