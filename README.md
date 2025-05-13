# DSP-PROJECT-Noise-Cancellation-Matlab-Code
[I wwrote this code in most efficient way better than everyone in my class]
A MATLAB program is needed to filter out low-energy signals from two different audio recordings containing both bird chirping and dog barking. By analyzing energy levels, the program should separate the dominant sound in each file—one containing only dog barking and the other only bird chirping. 

here is the perfect code:
clc;

[bird_audio, bird_sr] = audioread('4201.mp3');
[dog_audio, dog_sr] = audioread('344.wav');

[a, b] = butter(10, 2000 / (bird_sr / 2), 'high');
filtered_bird_audio = filter(a, b, bird_audio);
filtered_bird_audio = filtered_bird_audio / max(abs(filtered_bird_audio));

audiowrite('Filtered_Bird_Audio_167.wav', filtered_bird_audio, bird_sr);

[c, d] = butter(4, 1000 / (dog_sr / 2), 'low');
filtered_dog_audio = filter(c, d, dog_audio);
filtered_dog_audio = filtered_dog_audio / max(abs(filtered_dog_audio));

audiowrite('Filtered_Dog_Audio_167.wav', filtered_dog_audio, dog_sr);

disp('Playing filtered Bird Audio...');
sound(filtered_bird_audio, bird_sr);
pause(length(filtered_bird_audio) / bird_sr + 2);

disp('Playing filtered Dog Audio...');
sound(filtered_dog_audio, dog_sr);
