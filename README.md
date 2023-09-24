// users.h
#include <string>
#include <map>

class UserDatabase {
public:
  bool registerUser(const std::string& username, const std::string& password);
  bool authenticateUser(const std::string& username, const std::string& password); 
private:
  std::map<std::string, std::string> users; 
};

// users.cpp
#include "users.h"

bool UserDatabase::registerUser(const std::string& username, const std::string& password) {
  // Input validation
  if (username.empty() || password.empty()) {
    return false; 
  }

  // Check if username already exists
  if (users.find(username) != users.end()) {
    return false; 
  }

  users[username] = password;

  return true;
}

bool UserDatabase::authenticateUser(const std::string& username, const std::string& password) {
  // Input validation
  if (username.empty() || password.empty()) {
    return false;
  }

  // Check credentials
  if (users.find(username) != users.end() && users[username] == password) {
    return true;
  }

  return false;
}


// devices.h
#include <string>
#include <map>

class DeviceDatabase {
public:
  bool updateDeviceLocation(const std::string& deviceId, double latitude, double longitude);

private:
  std::map<std::string, std::pair<double, double>> deviceLocations; 
};

// devices.cpp
#include "devices.h"

bool DeviceDatabase::updateDeviceLocation(const std::string& deviceId, double latitude, double longitude) {
  // Input validation
  if (deviceId.empty()) {
    return false;
  }

  // Check if device exists
  if (deviceLocations.find(deviceId) != deviceLocations.end()) {
    deviceLocations[deviceId] = std::make_pair(latitude, longitude);
    return true;
  }

  return false;
}

// main.cpp
#include "users.h"
#include "devices.h"

int main() {
  UserDatabase userDB;
  DeviceDatabase deviceDB;

  // User registration
  if (userDB.registerUser("user1", "password")) {
    // success
  }

  // User authentication
  if (userDB.authenticateUser("user1", "password")) {
    // success
  }

  // Device location update
  if (deviceDB.updateDeviceLocation("device123", 37.7749, -122.4194)) {
    // success
  }

  return 0;
}
