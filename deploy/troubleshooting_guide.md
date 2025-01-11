# Troubleshooting Guide for GHL Chatbot Integration

## Common Issues & Solutions

1. **API Authentication Failures**
   - Check if GHL_LOCATION_ID matches the location in GoHighLevel
   - Verify PRIVATE_INTEGRATION_API_KEY is valid and not expired
   - Ensure API URL is correct for your region
   - Solution: Regenerate API keys if needed

2. **Message Handling Errors**
   - Contact not found errors: Ensure contact exists before sending messages
   - Rate limiting: Implement exponential backoff
   - Message format: Check payload structure matches API requirements
   - Solution: Log full request/response cycle for debugging

3. **Contact Creation Issues**
   - Duplicate contacts: Add checking before creation
   - Missing required fields: Validate input data
   - API validation errors: Check field format requirements
   - Solution: Implement pre-validation checks

4. **Scheduling Problems**
   - Timezone mismatches: Use UTC for all API calls
   - Availability conflicts: Check calendar before scheduling
   - Invalid datetime format: Use ISO 8601
   - Solution: Add timezone conversion handling

5. **Environment Setup**
   - Missing variables: Check all required vars are set
   - Wrong variable format: Follow exact format from docs
   - Production vs Development: Use correct endpoints
   - Solution: Use environment variable validation

## Quick Fixes

1. **Reset Integration**
   ```bash
   # Clear environment cache
   rm -rf .next
   # Reinstall dependencies
   npm install
   # Rebuild
   npm run build
   ```

2. **Debug Mode**
   ```javascript
   // Add to ghl-integration.ts
   const DEBUG = process.env.DEBUG === 'true';
   if (DEBUG) console.log('API Request:', request);
   ```

3. **API Health Check**
   ```javascript
   // Add to your integration
   async function checkAPIHealth() {
     try {
       const response = await fetch(PRIVATE_INTEGRATION_API_URL + '/health');
       return response.ok;
     } catch (error) {
       console.error('API Health Check Failed:', error);
       return false;
     }
   }
   ```

## Prevention Tips

1. **Input Validation**
   - Always validate user input before API calls
   - Check for required fields
   - Sanitize input data
   - Use TypeScript interfaces for type safety

2. **Error Logging**
   - Implement detailed error logging
   - Log API request/response cycles
   - Use unique error IDs for tracking
   - Set up error monitoring (e.g., Sentry)

3. **Testing**
   - Run integration tests before deployment
   - Test with various input scenarios
   - Verify error handling works
   - Check rate limit handling

4. **Monitoring**
   - Set up API health monitoring
   - Track API response times
   - Monitor rate limit usage
   - Set up alerts for failures

## Emergency Contacts

- GHL Support: support@gohighlevel.com
- Integration Team: team@julius.ai
- API Status: https://status.gohighlevel.com/
