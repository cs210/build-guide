+++
date = '2025-01-25T10:55:07-08:00'
draft = false
title = 'Mobile Basics'
weight = 1
+++
# Mobile Basics 

## Language choice 

For building a mobile app we would suggest using React Native. It renders native mobile componenets and almost all code can be shared between IOS and Android. 

If you want higher performance on a specific type of device it might be worth considering the use of a Swift(IOS) or Kotlin(Android).

## Developing and Running Apps 

We suggest that you use [expo](https://expo.dev/) to test your app throughout your development process. It's accessible and has everything your team will need most of the time. You can also write for both iOS and Android regardless of your development machine. 

If you need maximum flexibility, want to use or write specific, native modules, and/or have prior React Native and app development experience, consider React Native CLI.

## React Native Resources

For a simple step-by-step setup of React Native and Expo check out this [10 minute video](https://www.youtube.com/watch?v=YysKbNk1tj0).

For comprehensive learning resources check out the course resources for [CS 147L](https://www.youtube.com/watch?v=YysKbNk1tj0).

For in depth explanation check out the [React-Native documentation](https://reactnative.dev/docs/getting-started).

## React Native with Expo - Development Guide

### Development Enviroment Setup

#### Setup and Installation
First, check if you have Node installed. If not, download [Node](https://nodejs.org/en):  
```bash
node -v
```   
Then follow these commands:

```bash
# Install Expo CLI globally - this is like installing your main toolkit
npm install -g expo-cli

# Create a new Expo project - this creates a new folder with all the basic files you need
npx create-expo-app MyCapstoneProject

# Start development - this will open a development server
cd MyCapstoneProject
npx expo start
```

After running `npx expo start`, you'll see a QR code. Install the Expo Go app on your phone, scan this QR code, and you'll see your app running on your device!

#### Project Structure
Starting off with good organization makes future development easier. Here is a good starting folder structure:
```
MyCapstoneProject/
├── assets/           # Your app's images, fonts, and other files
├── components/       # Reusable pieces of your app's interface
├── screens/         # Full pages of your app
├── navigation/      # Code that handles moving between screens
├── hooks/           # Reusable logic
├── App.js           # The main file that starts your app
└── app.json         # Settings for your app
```

### Essential Components and Patterns

#### 1. Creating Your First Screen
A screen is like a full page in your app. Here's a basic example with explanations:

```jsx
// screens/HomeScreen.js
import { View, Text, StyleSheet } from 'react-native';
import { StatusBar } from 'expo-status-bar';

// This is your main screen component
const HomeScreen = () => {
  return (
    // View is like a <div> in web development - it's a container
    <View style={styles.container}>
      {/* StatusBar controls the top bar of the phone */}
      <StatusBar style="auto" />
      
      {/* Text is used for any text you want to display */}
      <Text style={styles.title}>Welcome!</Text>
    </View>
  );
};

// Styles in React Native are similar to CSS but with camelCase names
// They're defined using StyleSheet.create for better performance
const styles = StyleSheet.create({
  container: {
    flex: 1,  // This makes the container take up all available space
    padding: 16,
    alignItems: 'center',  // Center items horizontally
    justifyContent: 'center',  // Center items vertically
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
  },
});

export default HomeScreen;
```

#### 2. Navigation (Moving Between Screens)
Navigation is how users move between different screens in your app. Think of it like changing pages in a book:

```jsx
// navigation/AppNavigator.js
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';

// Stack navigation works like a stack of cards
// You can push new screens on top and pop them off to go back
const Stack = createNativeStackNavigator();

const AppNavigator = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        {/* Each Screen component is like a page in your app */}
        <Stack.Screen 
          name="Home" 
          component={HomeScreen}
          options={{ 
            title: 'Home',  // This appears at the top of the screen
            headerStyle: { backgroundColor: '#f4511e' },  // Customize the header
            headerTintColor: '#fff',  // Color of the header text
          }} 
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
};
```

#### 3. Working with Data (API Calls)
Most apps need to fetch data from the internet. Here's a reusable way to do that:

```jsx
// hooks/useApi.js
import { useState, useEffect } from 'react';

// This is a custom hook - a reusable piece of logic
const useApi = (url) => {
  // useState is used to store and update data
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  // useEffect runs when the component is first shown
  useEffect(() => {
    fetchData();
  }, [url]);

  // This function gets data from the internet
  const fetchData = async () => {
    try {
      const response = await fetch(url);
      const json = await response.json();
      setData(json);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  };

  return { data, loading, error };
};

// Example of using this hook in a component
const MyComponent = () => {
  const { data, loading, error } = useApi('https://api.example.com/data');

  // Show a loading spinner while waiting for data
  if (loading) return <ActivityIndicator />;
  // Show an error message if something went wrong
  if (error) return <Text>Error: {error}</Text>;
  
  // Show the data once it's loaded
  return <Text>{data.title}</Text>;
};
```

#### 4. Working with Images
Images are a crucial part of most apps. Here's how to handle them in Expo:

```jsx
// components/ProfileImage.js
import { Image } from 'react-native';
import { Asset } from 'expo-asset';

const ProfileImage = ({ uri }) => {
  return (
    // uri is the internet address of the image
    // The placeholder image shows while the main image is loading
    <Image
      source={{ uri }}
      style={{ width: 100, height: 100, borderRadius: 50 }}
      defaultSource={require('../assets/placeholder.png')}
    />
  );
};
```

#### 5. Storing Data Locally
Sometimes you need to save data on the device (like user settings or login information):

```jsx
// utils/storage.js
import * as SecureStore from 'expo-secure-store';

// Save data securely on the device
export const saveData = async (key, value) => {
  try {
    await SecureStore.setItemAsync(key, JSON.stringify(value));
  } catch (error) {
    console.error('Error saving data:', error);
  }
};

// Get data that was previously saved
export const getData = async (key) => {
  try {
    const value = await SecureStore.getItemAsync(key);
    return value ? JSON.parse(value) : null;
  } catch (error) {
    console.error('Error retrieving data:', error);
    return null;
  }
};
```

## Best Practices for Beginners

1. **Start Small**: Begin with a simple screen and add features gradually
2. **Use Console.log**: When something's not working, use console.log to print values and understand what's happening
3. **Test Frequently**: Make small changes and test them right away on your device
4. **Keep Components Small**: Break your screens into smaller, reusable components
5. **Learn from Errors**: Read error messages carefully - they often tell you exactly what's wrong

## Common Issues and Solutions

1. **App Not Updating**: Try restarting the Expo server (press 'r' in the terminal)
2. **Styling Not Working**: Make sure you're using the correct style properties (they're slightly different from CSS)
3. **Can't Connect to Device**: Ensure your phone and computer are on the same WiFi network
4. **Images Not Loading**: Double-check the image path and make sure the image exists

## Testing Your App

The easiest way to test your app is using the Expo Go app on your phone:
1. Start your development server (`npx expo start`)
2. Open Expo Go on your phone
3. Scan the QR code from your terminal
4. The app will load on your device

## Publishing Your App

When you're ready to share your app:
```bash
# Create a production version
expo build:android  # For Android
expo build:ios      # For iOS

# Test the production version
expo start --no-dev --minify

# Share your app through Expo
expo publish
```

## Getting Help

1. Check the [Expo Documentation](https://docs.expo.dev)
2. Leverage your favorite AI chatbot
2. Look for similar issues on Stack Overflow
3. Join the Expo Discord community

Remember: Everyone starts somewhere, and it's okay to make mistakes. The key is to learn from them and keep building!
