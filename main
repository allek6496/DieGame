# Stores the die and generates the next one. While there are repeats, it isn't a big deal because the numbers aren't super huge
class Die:
	# Stores the faces of the die
	faces = {'1': 0, '2': 0, '3': 0, '4': 0, '5': 0, '6': 0}
	
	# Stores the opposing die
	enemy = []

	# The greatest face on this die: sets when to move to the next digit
	maxFace = 0

	def __init__(self, enemy):
		self.enemy = enemy

		# Any face greater than one more than the biggest face on the opposing die is redundant, as once beaten, there's no need to beat it more. This is used to optimize the algorithm
		for face in enemy:
			if face > self.maxFace:
				self.maxFace = face;

	# Generates the next die, storing the value as a 6 digit base maxDigit-1 number and incrementing it
	def nextDie(self):
		if self.faces['1'] <= self.maxFace:
			self.faces['1'] += 1
		elif self.faces['2'] <= self.maxFace:
			self.faces['1'] = 0
			self.faces['2'] += 1
		elif self.faces['3'] <= self.maxFace:
			self.faces['1'] = 0
			self.faces['2'] = 0
			self.faces['3'] += 1
		elif self.faces['4'] <= self.maxFace:
			self.faces['1'] = 0
			self.faces['2'] = 0
			self.faces['3'] = 0
			self.faces['4'] += 1
		elif self.faces['5'] <= self.maxFace:
			self.faces['1'] = 0
			self.faces['2'] = 0
			self.faces['3'] = 0
			self.faces['4'] = 0
			self.faces['5'] += 1
		elif self.faces['6'] <= self.maxFace:
			self.faces['1'] = 0
			self.faces['2'] = 0
			self.faces['3'] = 0
			self.faces['4'] = 0
			self.faces['5'] = 0
			self.faces['6'] += 1
		# After it's done, return None
		else:
			return None
		return self.faces.values()

	# Returns the sum of the faces
	def total(self):
		return self.faces['1'] + self.faces['2'] + self.faces['3'] + self.faces['4'] + self.faces['5'] + self.faces['6']

	# The percent chance that you win against the oppising die
	def value(self):
		wins = 0
		ties = 0

		# Counts the number of possible tie and win states
		for face in self.faces.values():
			for vs in self.enemy:
				if face > vs:
					wins += 1
				elif face == vs:
					ties += 1
		# See the read-me for an explination
		return wins/(36-ties)

# For debugging purposes
## f = open("output.txt", "a+")
## F = open("process.txt", "a+")

# The opposing die
enemy = [4, 4, 4, 3, 3, 0]

die = Die(enemy)
bestDie = []
best = 0

# Loops through each die, stopping at the last one and storing the best scoring die
while True:
	attempt = die.nextDie()
	if attempt is None:
		break
	else:
		# Make sure that the sum of the faces is 18, a requirment of the problem but can easially be changed
		if die.total() == 18:
			## F.write(str(list(die.faces.values())) + ' ' + str(die.value()) + '\n')

			# If it's the new best die, then store it
			if die.value() > best:
				best = die.value()
				bestDie = list(die.faces.values());
				## f.write(str(list(die.faces.values())))
				## f.write(' ' + str(die.total()) + ' ' + str(die.value()) + '\n')

# Print result
print(best, list(bestDie))

## f.close()
## F.close()
